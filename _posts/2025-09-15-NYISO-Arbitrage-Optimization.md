---
layout: post
title: Arbitrage Optimization in NYISO
---

# Optimizing arbitrage in wholesale electricity markets, a toy example 
<br>
##### Arbitrage in wholesale electricity markets
<br>
The concept of arbitrage for battery storage in wholesale electricity markets is simple: ***buy low, sell high***. In practice this means charging when prices are low and discharging when prices are high. Optimization can allow us to determine the best possible charging and discharging schedule to maximize revenue.

##### How does arbitrage work?
<br>
In this toy example we start by looking at the day-ahead location-based marginal pricing (LBMP) prices for a particular reference bus over a three day period. A quick way to understand potential revenue is the price spread: the difference between the highest and lowest price. Larger spreads mean more arbitrage oppurtunity. Markets with more volatility, like ERCOT, often provide greater revenue potential.
<iframe src="{{ '/assets/images/DAM_arbitrage_example.html' | relative_url }}" 
        width="100%" 
        height="500" 
        style="border:none;">
</iframe>

##### How does the two settlement system work?
<br>
Arbitrage in wholesale electricity markets may sound simple but there are a couple complicating factors. NYISO, like many ISOs/RTOs, has a two settlement system: the Day-Ahead Market (DAM) and the Real-Time Market (RTM).

- **Day-Ahead Market (DAM):** Bids are placed one day in advanced based on a day-ahead load forecasts. Commitments to generate or consume electricity are financially binding, so generators are paid the contacted amount even if actual load is different than the forecast.
- **Real-Time Market (RTM):** This market deals with transactions in real-time to account for differences between the foreacted load and the actual load.  If the NYISO has not procured enough electricity in the DAM to meet actual demand it can then procure it in the real-time market. Similarly, if there is a surplus then that electricity can be sold. RTM operates in 5 minute intervals with 15 minute real-time commitments. RTM volumes tend to be smaller but prices are more volatile.

The plot below compares forecasted and actual load across NYISO over three days (not reference bus-specific).
<iframe src="{{ '/assets/images/forecasted_actual_load.html' | relative_url }}" 
        width="100%" 
        height="500" 
        style="border:none;">
</iframe>

A battery can participate in both markets: optimizing its day-ahead schedule, while also adjusting in real time when profitiable. The plot below shows DAM and RTM prices; note the greater volatility of RTM LBMPs.
<iframe src="{{ '/assets/images/day_ahead_and_rtm_prices' | relative_url }}" 
        width="100%" 
        height="500" 
        style="border:none;">
</iframe>

##### Why this is just a toy example
<br>
This post illustrates a simplified example of a hypothetical storage battery installed at a particular reference bus over three days. It is meant only for demonstration, not as a true revenue estimate. The goal is to showcase how mixed-integer linear programming (MILP) can be applied to opimize battery participation in NYISO markets. 

In this example we assume a 4-hour, 400 MWh battery with a 100 MW power rating. We assume a charge/discharge efficiency of 92%. The optimization determines charge/discharge schedule, state of charge, and which market the transactions take place in (DAM or RTM). A future post will dive into the technical details of how the optimization was implemented in Python with `cvxpy`.

The optimization seeks to maximize profit defined as: revenue from selling minus cost of buying across both markets. The constraints of the optimization are:
- The battery cannot simultaneously charge and discharge and must charge/discharge for at least an hour at a time
- The battery is subject to the physical specifications outlined for both physical and market behavior (ie. it cannot charge more than its capacity, but it also cannot bid for more than its capacity if it expects the actual load to be less)
- In the DAM market the battery cannot bid more than the hourly forecasted load
- In the RTM market the battery cannot bid for more than the forecast-actual load delta 
- In the RTM the battery charge/discharge commitments must be at 15 minute marks on the hour

##### Important disclaimers  
<br>
Here are some limitation to keep in mind:
- **Perfect forecast:** The battery "knows" all future prices, load forecasts, and actual loads. In reality, uncertainty makes optimization more complex and less profitable.
- **Perfect bids:** We assume the battery always clears the market and its bids do not affect prices. This is not a realistic assumption.
- **Brief time period:** This example covers a brief time period at one particular reference bus. In reality, price volatility can vary greatly. 
- **Energy market scope:** This toy battery only participates in energy markets and ignores capacity and ancillary services markets, which can be significant sources of storage revenue. In practice, we can optimize across all three markets. 

In summation, the optimal strategy presented is not actually achievable.

##### Optimal toy battery behavior
<br>
Breaking down the results by market, starting with the DAM, the plot below shows optimal DAM transactions. Even partial charges or discharges can be optimal depending on price changes. When the battery charges, cumulative revenue decreases, when it discharges, revenue increases, with the slope based on the price changes at each hour.
<iframe src="{{ '/assets/images/DAM_transactions_revenue.html' | relative_url }}" 
        width="100%" 
        height="500" 
        style="border:none;">
</iframe>
<br>
 
The next plot shows optimal RTM transactions. The behavior is similar to the DAM but prices are more erratic. In the RTM, batteries can only buy or sell as much electricity as the delta between the forecasted load and actual load; this is an additional constraint that does not apply to the DAM.
<iframe src="{{ '/assets/images/rtm_performance.html' | relative_url }}" 
        width="100%" 
        height="500" 
        style="border:none;">
</iframe>
<br>
Finally, this plot shows cumulative revenue over the three day period, with both DAM and RTM revenues contributing. In practice, no battery can perfectly exploid both markets at once, but optimization illustrates what's possible under idealized asumptions.The ***total optimal revenue*** for this period is: $41k. 
<iframe src="{{ '/assets/images/opt_performance.html' | relative_url }}" 
        width="100%" 
        height="500" 
        style="border:none;">
</iframe>
<br>

Once again, this is a simplified, illustrative toy example and does not reflect actual achievable revenues.

#### From toy example to real-world complexity
<br>
This toy example shows how optimization can guide battery behavior in NYISO's two settlement system. Optimizing revenue is not just about buying high and selling low as there is an oppurtunity cost to every transaction. Forecasting and optimization have the potential to improve revenue oppurtunities and reduce risk in battery investment.

Future posts will focus on:
1. **Implementation details**: optimization assumptions, constraints, and set-up
2. **Location impacts**: how siting affects results
3. **Forecasting**: predicting electricity prices and optimizing under uncertainty

Thank you for reading! 