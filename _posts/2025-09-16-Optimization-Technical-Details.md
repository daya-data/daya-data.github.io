---
layout: post
title: BESS Optimization Implementation 
---

# Behind the optimization: How the toy battery MILP works
<br>
This [previous post]({% post_url 2025-09-15-NYISO-Arbitrage-Optimization %}) walks through a simplified example of how a battery might optimize participation in NYISO’s day-ahead and real-time electricity markets. That post gave an overview of price spreads, the two-settlement system, and what optimal arbitrage looks like under idealized assumptions.

This follow-up goes into more implementation details of the optimization done in Python using [cvxpy](https://www.cvxpy.org/) for  mixed-integer linear programming (MILP) optimization.

#### Why MILP?
<br>
The goal of any form of arbitrage is to take advantage of changes in price to make money. This inherently lends itself to optimization as we seek to maximize an objective function while potential choices are subject to certain constraints.

The complexity of the market system, number of variables (when to charge/discharge, how much, and in which market), as well as the physics of the battery can be represented via an optimization problem. MILPs are useful because they allow us to capture both the continuous flows of energy and the discrete market commitments at the same time. That’s why they are an appropriate tool for battery arbitrage. `cvxpy` provides a clean way to express these constraints, while handling the actual MILP solvers like GLPK, CBC, or Gurobi.

#### Step 1: Defining the decision variables
<br>
The optimization decides on three main things:
1. **Day-Ahead actions** – how much to charge or discharge each hour
2. **Real-Time actions** – how much to adjust every 5 minutes
3. **State of Charge (SoC)** – the evolving energy level of the battery

#### Step 2: Defining the objective function
<br>
The objective function will be money made by the battery. The profit is the sum over time of price sold at ($/MWh) times power sold (MW) minus price bought at times power bought- applied to both markets. The optimizer tries to maximize revenue: 

```python
revenue_DA = cp.sum(p_DA * (d_DA - c_DA))
revenue_RT = dt * cp.sum(p_RT * (d_RT - c_RT))
objective = revenue_DA + revenue_RT
```
where `p_DA` is the price, `d_DA` is discharge quantity, and `c_DA` is charge quantity, with the same naming conventions for the real-time market. Keep in mind that DAM markets are hourly, whereas RTM markets are in 5 minute intervals therefore we include that in the calculation since LBMPs are in terms of $/MWh. That’s the “buy low, sell high” expressed mathematically.

#### Step 3: Defining constraints
<br>
The behavior of a battery in a wholesale electricity marketplace is governed by the physics of the battery as well as the rules of the marketplace. These are then translated into constraints within our optimization framework.

##### Physical Constraints

A battery is a physical system. It stores energy in MWh and delivers power in MW. Its state of charge (SoC) evolves based on charging and discharging decisions. It is limited by its total capacity, power rating at which it can charge and discharge, and efficiency in doing so.

The actions of the battery are constrained by:
```python
constraints += [
     c_DA[h] <= p_max * uc_DA[h],
     d_DA[h] <= p_max * ud_DA[h], 
     uc_DA[h] + ud_DA[h] <= 1,  # no simultaneous charging and discharging 
     c_DA[h] <= p_max, # charging/discharging 
     d_DA[h] <= p_max
]
```
where `c_DA` and `d_DA` are charging/discharging behavior, `p_max` is the physical power rating of the battery, and `uc_DA` is the binary charging on/off switch.

The SoC is the amount of charge in the battery at any given time. When the battery discharges, the SoC will decrease, when it charges the SoC will increase. But it is constrained by the physical limits of the battery as well as recommendations to not go all the way down to 0% or up to 100%. This constraint is expressed as: 

```python
constraints += [
    soc_DA[h+1] == soc_DA[h] + eta_c * c_DA[h] - (d_DA[h] / eta_d)
]
```
Here, `eta_c` and `eta_d` represent round-trip efficiency losses.

##### Market Constraints

There are constraints and rules associated with which actions the battery can take in the day-ahead and real-time markets. This toy model includes simplified versions of NYISO rules such as: 

* **Day-Ahead:** You can’t bid more MW than the load forecast.
* **Real-Time:** Every 15-minute block must stick to a single mode (charging or discharging), and you can only move electricity equal to the forecast/actual load delta.

To illustrate one of the constraints, here’s how a 5-minute step is constrained by the load delta in the real-time market: 

```python
if delta_load_5min[t] > 0:
    # only charging allowed, up to the delta
    d_RT[t] == 0
    c_RT[t] <= delta_load_5min[t]
elif delta_load_5min[t] < 0:
    # only discharging allowed
    c_RT[t] == 0
    d_RT[t] <= -delta_load_5min[t]
```

#### Where is the data coming from?
<br>
In addition to the hypothetical parameters of the battery and the NYISO market rules, optimizing arbitrage revenues also depends on the following data sources: 
- Day-ahead market prices
- Real-time market prices
- Day-ahead forecasted load
- Real-time actual load

These all come from NYISO publicly available [data](https://www.nyiso.com/energy-market-operational-data).

#### Results and what’s next
<br>
Running this toy example produces a charge/discharge schedule from which you can extrapolate a cumulative revenue curve like those shown in the previous post. Of course, real-world challenges (forecasting uncertainty, imperfect bids, market interactions) make things far trickier.

Upcoming posts will cover: 

* **Location matters** – how siting impacts revenue potential
* **Forecasting under uncertainty** – how to optimize when you *don’t* know future prices
* **Going beyond just arbitrage** – adding capacity and ancillary services markets into the mix

Feel free to reach out if you would like more details about the reference bus that was used in the example.


