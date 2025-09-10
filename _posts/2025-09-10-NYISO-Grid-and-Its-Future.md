---
layout: post
title: NYISO Grid and Its Future

---

# From Generators to Batteries: the NYISO Grid and Its Future
<br>

##### What is NYISO?
<br>
NYISO is the entity responsible for maintaining reliability and managing operations of the New York State electricity system. The grid consists of:

* **Generators**: produce electricity (fossil fuels, renewables, nuclear).  
* **Transmission networks**: transport electricity across the state   
* **Distribution systems**: transport electricity to the actual consumers  
* **Utilities and load-serving entities**: this is who coordinates the actual delivery and sells electricity to the consumers   
* **Consumers**: where the load demand is coming from 

NYISO coordinates this market to ensure that supply from generators meets demand from consumers with reliability and cost-effectiveness.

##### Observations & Trends in NYISO
<br>
The map below shows all market generators in the NYISO market<sup>[1](https://www.nyiso.com/documents/20142/2226333/2025-Gold-Book-Public.pdf)</sup>. Each circle shows the generator with its size corresponding with its summer capability and color corresponding to the type of generator. Broadly speaking: there are more fossil fuel generators downstate whereas renewables especially hydro tends to be concentrated upstate. 

<iframe src="{{ '/assets/maps/nyiso_generators.html' | relative_url }}" 
        width="100%" 
        height="500" 
        style="border:none;">
</iframe>

NYISO's analysis<sup>[2](https://www.nyiso.com/documents/20142/2223020/2025-Power-Trends.pdf)<sup> has outlined several trends: 

* **Electrification**: New York’s building decarbonization policies and electrification of heating will increase electricity demand.  
* **Large new loads**: Growth of data centers and AI/LLM workloads could substantially increase peak demand.  
* **Aging fossil retirements**: As older fossil units retire without immediate replacements, supply margins tighten

This tells us there will be *increasing load demand* with ***decreasing supply capability***-this puts NYISO in a tighter spot. NYISO forecasts that New York will soon become a ***winter-peaking system***—meaning annual peak demand will occur in winter (due to heating loads) rather than in summer (air conditioning).

##### How Does NYISO Manage the Grid?
<br>
NYISO manages electricity through three markets: energy markets, ancillary markets, and capacity markets. 

**Energy Markets**

* **Day-Ahead Market (DAM)**: Generators submit bids the day before (e.g., “X MW at $Y/MWh”). NYISO runs an optimization to meet this demand with the cheapest combination of bids from generators using a market clearing system but taking into account transmission constraints.  
* **Real-Time Market (RTM)**: Operates on a shorter time frame to deal with differences between day-ahead forecasts and real-world conditions.

The prices paid out to generators are ***nodal*** meaning based on the specific node associated with the location; whereas the price paid by the consumer are ***zonal*** meaning aggregated average of multiple nodal prices across a zone. One important caveat is that battery storage will be paid and pay the nodal prices *unless* they are behind-the-meter batteries which will buy from the utility and discharge for a more target purpose. 

Each location’s nodal price is called the ***Locational-Based Marginal Price (LBMP)***, which accounts for:

LBMP = Marginal Energy Price + Marginal Loss Price + Marginal Congestion Price


The marginal energy price is the highest price for the next generator to meet supply. The loss component accounts for loss along the transmission path for reasons such as heat dissipation. Transmission limits (thermal, voltage, stability) influence congestion costs. Transporting electricity from long distances (such as from upstate to downstate) can approach limits of transmission lines and require the grid to buy more expensive electricity that is produced closer by or along less congested transmission lines. 

**Ancillary Services Markets**

This market is intended to ensure reliability without actually contributing towards demand, instead ensuring proper frequency, voltage, and reserves for the grid. Some services are ***cost-based*** whereas others are ***market-based*** meaning that suppliers submit bids to meet ancillary service needs in a similar manner to the energy markets

**Capacity Markets**

Unlike ERCOT or CAISO, NYISO has a ***capacity market*** to ensure long-term reliability. Resources are procured months to years in advance to guarantee that forecasted peak load plus a reserve margin can always be met.

For example, the Installed Capacity (ICAP) requirement for 2025/2026 is a ***24.4% reserve margin***, with location-specific requirements ensuring resources are available where they’re most needed.

##### Investment and the Role of BESS
<br>
Battery Energy Storage Systems (BESS) can profit via arbitrage, meaning charging the battery when the price of electricity is low (such as at night) and then selling that electricity when the price is high (perhaps when demand is higher during the evening peak). However for NYISO there are also opportunities in the capacity and ancillary services markets. 

In markets with high price volatility (like ERCOT or CAISO), arbitrage alone can be lucrative. NYISO’s lower volatility makes optimization across the three markets a better approach. This means optimization also in regards to battery size and location, decreasing risk by operating across multiple markets. This creates opportunities for investors who use ***forecasting and optimization models*** to minimize risk and maximize returns.

##### Grid Stability, Decarbonization, and Policy
<br>
NYISO’s future is closely tied to New York State’s ***climate and clean energy goals***. Policies targeting emissions reductions, renewable integration, and fossil retirements put pressure on the system to balance reliability with decarbonization.

BESS is a necessary component to reduce reliance on fossil fuels, ensure grid reliability, and enable use of intermittent renewable energy. BESS and renewable investments play a critical role in this transition, but require:

A strong understanding of NYISO’s market systems.  
Sophisticated modeling tools to forecast demand, prices, and bidding behavior.  
Optimization approaches to determine where and how resources should participate.

##### Looking Ahead
<br>
Future posts will cover:

* **Forecasting**: energy prices, demand by subregion, bidding behavior, fuel prices, and weather impacts.  
* **Optimization**: strategies for arbitrage, capacity, and ancillary services across different battery sizes and sites 

Understanding the NYISO market structure can help us quantify electricity opportunities and risks in the future. 

<br>

<sup>1</sup>[NYISO 2025 Gold Book](https://www.nyiso.com/documents/20142/2226333/2025-Gold-Book-Public.pdf)  
<sup>2</sup>[NYISO 2025 Power Trends Report](https://www.nyiso.com/documents/20142/2223020/2025-Power-Trends.pdf)  

