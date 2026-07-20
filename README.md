# Freight Cost Minimization Supply Chain Logistics Brunel - Operations Research Project

[![Operations Research](https://img.shields.io/badge/Operations_Research-2E7D32?style=for-the-badge)]()
[![Optimization Algorithm](https://img.shields.io/badge/Optimization_Algorithm-1565C0?style=for-the-badge)]()
[![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white)](https://www.python.org/)
[![Pandas](https://img.shields.io/badge/Pandas-150458?style=for-the-badge&logo=pandas&logoColor=white)](https://pandas.pydata.org/)
[![NumPy](https://img.shields.io/badge/NumPy-013243?style=for-the-badge&logo=numpy&logoColor=white)](https://numpy.org/)
[![Matplotlib](https://img.shields.io/badge/Matplotlib-11557C?style=for-the-badge)](https://matplotlib.org/)
[![PuLP](https://img.shields.io/badge/PuLP-F28C28?style=for-the-badge)](https://coin-or.github.io/pulp/)
[![Jupyter](https://img.shields.io/badge/Jupyter-F37626?style=for-the-badge&logo=jupyter&logoColor=white)](https://jupyter.org/)
[![Anaconda](https://img.shields.io/badge/Anaconda-44A833?style=for-the-badge&logo=anaconda&logoColor=white)](https://www.anaconda.com/)
[![Excel](https://img.shields.io/badge/Microsoft_Excel-217346?style=for-the-badge&logo=excel&logoColor=white)]()
[![Markdown](https://img.shields.io/badge/Markdown-000000?style=for-the-badge&logo=markdown&logoColor=white)](https://www.markdownguide.org)
[![GitHub](https://img.shields.io/badge/GitHub-181717?style=for-the-badge&logo=github&logoColor=white)](https://github.com)

## 📌 Overview

*Operations Research Project - Freight Cost Minimization Supply Chain Logistics Brunel* aims to provide a business solution for Minimizing Freight Carrier Transportation Costs by constructing **Optimization Model** using **Linear Programming (LP) Simplex Method** in Operations Research. The Mathematical Optimization Model determines the most cost-efficient carrier assignment by considering operational and transportation constraints. Deployed using **PuLP (CBC Solver)**, the Optimization Model integrates **Decision Variables**, **Objective Function**, and **Constraints** to obtain the optimal solution. The Model combines **Customer Orders, Carrier Availability , Freight Rates, Transportation Routes, and Service-Level** requirements to identify optimal shipment allocation strategy.

## 📂 Repository Structure

```
OR-Project_SupplyChainLogisticBrunel
│
├── README.md                                     ← README
│
├── data                                          ← Datasets Used For This Project
│   └── supply_chain.xlsx
│
├── results                                       ← All Results and Analysis CSV Files
│   ├── carrier_summary.csv
│   ├── dual_price.csv
│   ├── mode_summary.csv
│   ├── optimal_assignment.csv
│   ├── optimal_strategy.csv
│   └── OR_LP_SupplyChainLogisticBrunel.pbix
│
└── src                                           ← Source Code
    └── OR_LP_SupplyChainLogisticBrunel.ipynb     ← Linear Programming Optimization Model
```

## 📊 Dataset 

The Dataset is sourced from the [Supply Chain Logistics Problem Dataset by Brunel University](https://brunel.figshare.com/articles/dataset/Supply_Chain_Logistics_Problem_Dataset/7558679/2?file=20162015) on Brunel University Official Repository Website. It is a publicly available Supply Chain Logistics Dataset developed by Brunel University London researchers for transportation planning and optimization implementation The complete datasets consists of 7 worksheets each representing a different component of the Supply Chain Network and covering the Operational Data, which titled OrderList, FreightRates, WhCosts, WhCapacities, ProductsPerPlant, VmiCustomers, and PlantPorts. For this project, Optimization Model focuses **Minimizing Freight Transportation Cost**. Therefore, only the **OrderList** and **FreightRates** worksheets are used to formulate the Linear Programming Model as they contain the Customers Demand, Carrier Options, Transportation Routes, and Freight Rate Information as variables required for Optimization.

| OrderList Table | Description |
|---|---|
| `Order ID` | Unique ID Assigned To Each Customer Order |
| `Order Date` | Date Which Customer Order Was Placed |
| `Origin Port` | First Port Which Shipment Is Dispatched (Depot) |
| `Carrier` | Transportation Carrier To Deliver The Shipment |
| `TPT` | Transportation Delivering Process For Shipment |
| `Service Level` | Shipment Service Level Category For Delivery Speed |
| `Ship ahead day count` | Day Count For Early Arrival Shipment |
| `Ship Late Day count` | Day Count For Late Arrival Shipment |
| `Customer` | Unique ID Assigned To Each Customer |
| `Product ID` | Unique ID Assigned To Each Product Order |
| `Plant Code` | Manufacturing Plant or Warehouse Supplying The Product |
| `Destination Port` | Final Port Shipment Which Customer Destination |
| `Unit quantity` | Product Unit Count Ordered |
| `Weight` | Total Product Weight Ordered |

| FreightRates Table | Description |
|---|---|
| `Carrier` | Transportation Carrier To Deliver The Shipment |
| `orig_port_cd` | First Port Which Shipment Is Dispatched (Depot) |
| `dest_port_cd` | Final Port Shipment Which Customer Destination |
| `minm_wgh_qty` | Minimum Weight Required For Chosen Freight Rate|
| `max_wgh_qty` | Minimum Weight Required For Chosen Freight Rate |
| `svc_cd` | Shipment Service Level Category For Delivery Speed |
| `minimum cost` | Minimum Delivery Rate Applied |
| `rate` | Freight Delivery Rate As Cost Per Unit Of Weight |
| `mode_dsc` | Transportation Mode |
| `tpt_day_cnt` | Estimated Transportation Delivery Day Count |
| `Carrier type` | Transportation Carrier Category |

## 🧠 Analyses


1.    **Operations Research Freight Cost Optimization:** Determines optimal solution of Minimizing Freight Cost of Supply Chain Logistics Problem. 

2.    **Exploratory Data Analysis:** Focusing on OrderList and FreightRates tables, the analysis identified a total of 9,215 orders registered in OrderList table and 1,540 valid Freight Rates available across 9 carrier option in FreightRates table. Since FreightRates table only provides pricing for DTD and DTP Shipment Service Level Category For Delivery Speed, orders with CRF Service Level were excluded, resulting in 8,361 orders included in the Optimization Model. Considering each unique combination of Origin Port, Destination Port, and Service Level with available Carrier options, the analysis identified 3 feasible Transportation Routes:

| Origin Port | Destination Port | Service Level |
|---|---|---|
| PORT09 | PORT09 | DTP |
| PORT04 | PORT09 | DTP |
| PORT04 | PORT09 | DTD |

3.    **OrderxCarrier Options:** Every feasible OrderxCarrier combinations were generated to establish the decision variables for Optimization Model. To improve timestamp and computational efficiency, data sampling are applied in creating a random sample of 500 orders selected from OrderList table. The sampling generated 1,924 feasible OrderxCarrier combinations with each order having an average of 3-4 eligible Carrier options.

4.    **Decision Variables:** Decision Variables of the Linear Programming Optimization Model defines a total of 839 Order-Carrier unique combination options and a binary  type. Decision Variables are represented as:

$$
x_{0,v444_0} , x_{1,V444_8} , x_{1,V444_0} , ... , x_{498,V444_0} , x_{498,V444_4} , x_{499,V444_0}
$$

5.    **Objective Function:** Obtained an Objective Function formulated from:

$$
Max(MinimumCost , Rate*Weight)
$$

Objective Function is represented as:

$$
\begin{aligned}
\min Z =\&
2.9984x_{0,v444_0} + 6.9104x_{100,v444_0} + 39.1432265407602x_{100,v444_4} + ... + \\
&7.887861583412498x_{98,v444_0} + 2.9984x_{99,v444_0} + 2.9984x_{9,v444_0}\\
\end{aligned}
$$

6.    **Constraints:** Constraints of the Linear Programming Optimization Model defines a total of 500 constraints which represented as:

$$
\begin{aligned}
x_{0,V444_0} &= 1\\
x_{1,V444_0} + x_{1,V444_4} + x_{1,V444_8} &= 1\\
x_{2,V444_0} &= 1\\
\\
... &...\\
\\
x_{499,V444_0} &= 1
\end{aligned}
$$

7.    **Linear Programming Model:** Constructed the Linear Programming Model by using the PuLP library PULP_CBC_CMD() solver by integrating the Decision Variables, Objective Function, and Constraints into the model to obtain the Optimal Freight Allocation Strategy.

8.    **Optimal Solution:** The Linear Programming Model reached an Optimal Solution achieving a Minimum Total Freight Transportation Cost of $2,917.8564 for 500 sampled orders.

## 💡 Key Findings Summary

- **Achieve Optimal Solution With Significant Cost Reduction:** Linear Programming Optimization Model identified the globally optimal carrier assignment and reducing total Transportation Costs by 60.5%

| Optimal Strategy | Cost (500 Orders) | Cost (8,361 Orders) | Savings To Historical |
|---|---|---|---|
| Historical (Most Expensive) | $7,390.8405 | $123,590 | Baseline |
| Greedy (Most Cheap) | $2,029.8760 | $33,944 | $5,360.9645 |
| Linear Programming Simplex Optimal | $2,917.8564 | $48,792 | $4,472.9841 (60.5%) |

- **Optimization Balanced Cost Efficiency with Operational Feasibility:** Compared to Greedy Method which only consider the lowest-cost carrier for each shipment, Linear Programming Optimization Model generated an optimal solution by considering all Operational Constraints emerges in the business, ensuring every shipment received a feasible carrier assignment.

- **Mathematical Optimization Scales Decision-Making Across the Supply Chain:** Rather than only evaluating shipments into the formula, the Optimization Model evaluted all feasible Order-Carrier combinations as a complete Optimization Problem which leads to Decision Variable. The Optimization Model enabled a consistent and data-driven carrier assignments that could be scaled to larger Transportation Networks and additional Business Constraints.

## 👤 About The Author

**Arruum Pratistha Kiranadjie**     
Data Analyst | Quantitative Analyst | Operations Research Analyst

Quantitative Analyst experiences in Data Analysis, Operations Research, and Quantitative Research Analysis. Proficient in Mathematical Modeling and Database Management leveraging Prediction and Optimization Algorithms to solve complex real-world problems.

- [LinkedIn: Arruum Kiranadjie](https://www.linkedin.com/in/arruumkiranadjie)
- [GitHub: Arruum Kiranadjie](https://github.com/arruumkiranadjie)
- [Tableau: Arruum Kiranadjie](https://public.tableau.com/app/profile/arruum.kiranadjie/vizzes)

© 2026 Arruum Kiranadjie. All rights reserved.
