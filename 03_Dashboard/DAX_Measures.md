# DAX Measures Documentation

## Overview

This document contains all DAX measures used in the **Adventure Works: Profitability & Commercial Performance Analytics** project.

Measures are classified according to the KPI framework established during dashboard planning:

* **Outcome Measures** 
* **Diagnostic Measures** 
* **Supporting Measures** 

---

# Outcome Measures

These measures represent the primary business outcomes monitored by the Profitability Analysis Stakeholder.

| DAX Measure      | DAX Formula                                                                              | 
| ---------------- | ---------------------------------------------------------------------------------------- | 
| Profit           | `Profit = [Revenue] - [Cost]`                                                            |
| Profit Margin %  | `Profit Margin % = DIVIDE([Profit], [Revenue]) * 100`                                       |
| Revenue Growth % | `Revenue Growth % = DIVIDE([H1 2017 Revenue] - [H1 2016 Revenue], [H1 2016 Revenue]) * 100` |

---

# Diagnostic Measures

These measures explain why Profit, Profit Margin %, and Revenue Growth % change over time.

| DAX Measure            | DAX Formula                                                                                                |
| ---------------------- | ---------------------------------------------------------------------------------------------------------- | 
| Revenue                | `Revenue = SUMX(sales, sales[OrderQuantity] * RELATED(products[ProductPrice]))`                            |  
| Cost                   | `Cost = SUMX(sales, sales[OrderQuantity] * RELATED(products[ProductCost]))`                                |  
| Orders                 | `Orders = DISTINCTCOUNT(sales[OrderNumber])`                                                               |  
| Units Sold             | `Units Sold = SUM(sales[OrderQuantity])`                                                                   |  
| AOV                    | `AOV = DIVIDE([Revenue], [Orders])`                                                                     |  
| ASP                    | `ASP = DIVIDE([Revenue], [Units Sold])`                                                                 |  
| ARPC                   | `ARPC = DIVIDE([Revenue], [Customer Count])`                                                            |  
| Return Quantity        | `Return Quantity = SUM(returns[ReturnQuantity])`                                                           |  
| Return Value           | `Return Value = SUMX(returns, returns[ReturnQuantity] * RELATED(products[ProductPrice]))`                  |  
| Return Rate %          | `Return Rate % = DIVIDE([Return Quantity], [Units Sold]) * 100`                                               |  
| Net Revenue            | `Net Revenue = [Revenue] - [Return Value]`                                                                 |  
| Revenue Contribution % | `Revenue Contribution % = DIVIDE([Revenue], CALCULATE([Revenue], ALL(products))) * 100`                       |  
| Mix Shift              | `Mix Shift = [Revenue Contribution %] - CALCULATE([Revenue Contribution %], DATEADD(calendar[Date], -1, YEAR))` |  

---

# Supporting Measures

These measures provide analytical context and support calculations used by higher-level KPIs.

| DAX Measure     | DAX Formula                                                                                                           |
| --------------- | --------------------------------------------------------------------------------------------------------------------- |
| Customer Count  | `Customer Count = DISTINCTCOUNT(sales[CustomerKey])`                                                              |
| H1 2016 Revenue | `H1 2016 Revenue = CALCULATE([Revenue], FILTER(ALL('calendar'), calendar[Date] >= DATE(2016, 1, 1) && calendar[Date] <= DATE(2016, 6, 30))` |
| H1 2017 Revenue | `H1 2017 Revenue = CALCULATE([Revenue], FILTER(ALL('calendar'), calendar[Date] >= DATE(2017, 1, 1) && calendar[Date] <= DATE(2017, 6, 30))` |

---

# Measure Dependency Hierarchy

```text
Outcome Measures
│
├── Profit
│   ├── Revenue
│   └── Cost
│
├── Profit Margin %
│   ├── Profit
│   └── Revenue
│
└── Revenue Growth %
    ├── H1 2016 Revenue
    └── H1 2017 Revenue

Diagnostic Measures
│
├── Revenue
├── Cost
├── Orders
├── Units Sold
├── Return Quantity
├── Customer Count
│
├── AOV
│   ├── Revenue
│   └── Orders
│
├── ASP
│   ├── Revenue
│   └── Units Sold
│
├── ARPC
│   ├── Revenue
│   └── Customer Count
│
├── Return Value
│   └── Return Quantity
│
├── Return Rate %
│   ├── Return Quantity
│   └── Units Sold
│
├── Net Revenue
│   ├── Revenue
│   └── Return Value
│
├── Revenue Contribution %
│   └── Revenue
│
└── Mix Shift
    └── Revenue Contribution %
```

---

# Notes

* Revenue is derived using **Product Price × Order Quantity**.
* Cost is derived using **Product Cost × Order Quantity**.
* Profit is derived and is not stored directly in the dataset.
* Revenue Growth % uses **H1 2017 vs H1 2016** to account for the dataset ending on **30 June 2017**.
* Customer Count is based on purchasing customers (`sales[CustomerKey]`) to ensure ARPC reflects revenue per active customer rather than all customers in the master table.
* Return analysis is limited to product, category, and regional levels because customer-level return information is unavailable.
* All measures were validated against source data and dashboard outputs during the dashboard validation phase.
