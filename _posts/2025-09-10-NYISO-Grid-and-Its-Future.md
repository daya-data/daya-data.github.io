---
layout: post
title: NYISO Grid and Its Future

---

# From Generators to Batteries: the NYISO Grid and Its Future
<br>

##### What is NYISO?
<br>
NYISO is the entity responsible for maintaining reliability and managing operations of the New York State electricity system. The system consists of:

* **Generators**: produce electricity (fossil fuels, renewables, nuclear).  
* **Transmission networks**: transport electricity across the state   
* **Distribution systems**: transport electricity to consumers  
* **Utilities and load-serving entities**: coordinate the delivery and sale of electricity to consumers   
* **Consumers**: produce demand for electricity 

NYISO coordinates this market to ensure that supply from generators meets demand from consumers with reliability and cost-effectiveness.

##### Observations & Trends in NYISO
<br>
The map below shows all market generators in the NYISO energy market<sup>[1](https://www.nyiso.com/documents/20142/2226333/2025-Gold-Book-Public.pdf)</sup> in 2024. Broadly speaking: there are more fossil fuel generators downstate whereas renewables especially hydro tends to be concentrated upstate. 

<iframe src="{{ '/assets/maps/nyiso_generators.html' | relative_url }}" 
        width="100%" 
        height="500" 
        style="border:none;">
</iframe>
<br>

NYISO's analysis<sup>[2](https://www.nyiso.com/documents/20142/2223020/2025-Power-Trends.pdf)</sup> has outlined several trends: 

* **Electrification**: New York’s building decarbonization policies and electrification of heating will increase electricity demand
* **Large new loads**: Growth of data centers and AI/LLM workloads _could_ significantly increase peak demand
* **Aging fossil retirements**: As older fossil units retire without immediate replacements, supply margins tighten


We can anticipate ***increasing load demand*** with ***decreasing supply capability***, putting NYISO in a tighter spot. NYISO forecasts that New York will soon become a ***winter peaking system***—meaning annual peak demand will occur in winter due to heating loads rather than in the summer.

##### How Does NYISO Manage the Grid?
<br>
NYISO coordinates electricity through three markets: energy, ancillary, and capacity. 

**Energy Markets**

* **Day-Ahead Market (DAM)**: Generators submit bids the day before (e.g., “X MW at $Y/MWh”) and then  NYISO runs an optimization to meet this demand with the cheapest combination of generators while taking into account transmission constraints.  
* **Real-Time Market (RTM)**: Deals with differences between day-ahead forecasts and real-world conditions.

The prices paid out to generators are ***nodal*** meaning based on the specific node associated with the location; whereas the price paid by the consumer are ***zonal*** meaning aggregated average of multiple nodal prices across a zone. One important caveat is that battery storage will be paid and pay the nodal prices *unless* they are behind-the-meter batteries which will buy from the utility and discharge for a more target purpose. 

Each location’s nodal price is called the ***Locational-Based Marginal Price (LBMP)***, which accounts for:

LBMP = Energy + Loss - Congestion

The marginal energy price component is the price of the most expensive generator needed to meet demand. The marginal loss price component accounts for loss along the transmission for reasons such as heat dissipation. The marginal congestion component accounts for transmission limits (thermal, voltage, stability) which might require more expensive generators to be used.

The plot below shows the components of the wholesale electricity prices paid to Astoria Energy's natural gas generator in Queens, NY.

<iframe src="{{ '/assets/images/323677.html' | relative_url }}" 
        width="100%" 
        height="500" 
        style="border:none;">
</iframe>

**Ancillary Services Markets**

This market is intended to ensure reliability without contributing towards load, instead ensuring proper frequency, voltage, and reserves for the grid. Some services are ***cost-based*** whereas others are ***market-based*** meaning that suppliers submit bids to meet ancillary service needs in a similar manner to the energy markets

**Capacity Markets**

Unlike ERCOT and CAISO, NYISO has a ***capacity market*** to ensure long-term reliability. Resources are procured months to years in advance to guarantee that forecasted peak load plus a reserve margin can always be met.For example, the Installed Capacity (ICAP) requirement for 2025/2026 is a ***24.4% reserve margin***, with requirements for where this capacity must be located.

##### Investment and the Role of BESS
<br>
Battery Energy Storage Systems (BESS) can profit via arbitrage, meaning charging the battery when the price of electricity is low (such as at night) and then selling when the price is high (during the evening peak). However for NYISO there are also opportunities in the capacity and ancillary services markets. 

In markets with high price volatility (like ERCOT), arbitrage alone can be lucrative. NYISO’s lower volatility makes optimization across the three markets a better approach, considering the role of battery size and site location. This creates opportunities for investors who use ***forecasting and optimization models*** to minimize risk and maximize returns.

##### Grid Stability, Decarbonization, and Policy
<br>
NYISO’s future is closely tied to New York State’s ***climate and clean energy goals***. Policies targeting emissions reductions, renewable integration, and fossil retirements put pressure on the system to balance reliability with decarbonization.

BESS is a necessary component to reduce reliance on fossil fuels, ensure grid reliability, and enable use of intermittent renewable energy. BESS and renewable investments play a critical role in this transition, but require:

* A strong understanding of NYISO’s market systems
* Sophisticated modeling tools to forecast demand, prices, and bidding behavior 
* Optimization approaches to determine where and how resources should participate

##### Looking Ahead
<br>
Future posts will cover:

* **Forecasting**: energy prices, demand by subregion, bidding behavior, fuel prices, and weather impacts
* **Optimization**: strategies for arbitrage, capacity, and ancillary services across different battery sizes and sites 

Understanding the NYISO market structure can help us quantify electricity opportunities and risks in the future. 

<br>

<sup>1</sup>[ NYISO 2025 Gold Book](https://www.nyiso.com/documents/20142/2226333/2025-Gold-Book-Public.pdf)  
<sup>2</sup>[ NYISO 2025 Power Trends Report](https://www.nyiso.com/documents/20142/2223020/2025-Power-Trends.pdf)  

