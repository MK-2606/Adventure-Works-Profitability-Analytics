# Adventure Works Profitability & Commercial Performance Analytics

## Project Overview

This project analyzes Adventure Works sales, returns, customer, product, and territory data to evaluate business performance through three strategic lenses:

- Revenue Growth
- Profitability
- Revenue Quality

The objective was to support a Profitability Analysis Stakeholder in understanding not only how the business is performing, but why performance is changing and where corrective action or investment should be directed.

---

## Business Problem

Revenue growth alone does not guarantee business success.

A business can experience:

- Margin erosion
- Rising costs
- Product profitability issues
- Return-related revenue leakage
- Regional underperformance

This project was developed to determine whether commercial growth was translating into sustainable profitability.

---

## Stakeholder

### Profitability Analysis Stakeholder

**Responsibilities:**

- Monitor financial performance
- Evaluate commercial efficiency
- Improve profitability
- Allocate resources effectively
- Support growth initiatives

---

## Business Questions

### Growth Analysis

1. How does monthly revenue and order volume vary across the year, and are seasonal patterns consistent across 2015–2017?
2. What is the revenue contribution by product category, and how has category-level mix shifted over time?
3. What is the Average Order Value (AOV) trend, and how do AOV and Order Volume contribute to Revenue growth over time?

### Regional Analysis

4. Which regions are driving or dragging overall revenue, and has that pattern shifted across the three years?

### Returns Analysis

5. What is the return rate by product category, does it correlate with order volume, and does it vary significantly across territories?
6. Are high-return products also high-revenue products, and what does that imply for net revenue?

### Customer Analysis

7. Which customer segments generate the highest revenue, and are they growing or shrinking?

### Product & Profitability Analysis

8. Which products have high volume but low revenue contribution?
9. Which products have high revenue but low profit?
10. Which products, categories, and regions generate the highest profit?
11. Are we growing revenue at the expense of profitability?

---

## KPI Framework

### Outcome KPIs

| KPI | Purpose |
|------|----------|
| Profit | Measures value creation after product-related costs |
| Profit Margin % | Measures efficiency of converting revenue into profit |
| Revenue Growth % | Measures commercial expansion over time |

### Diagnostic Metrics

- Revenue
- Cost
- Orders
- AOV
- ASP
- ARPC
- Revenue Contribution %
- Return Rate %
- Net Revenue
- Mix Shift
- Customer Count

### Supporting Metrics

- Product Category
- Product
- Region
- Customer Segment
- Month
- Year

---

## Dataset Information

| Item | Details |
|--------|---------|
| Dataset | Adventure Works |
| Date Range | 1 January 2015 – 30 June 2017 |
| Total Sales Records | 56,046 |
| Modeling Approach | Hybrid Dimensional Model |
| Fact Tables | Sales, Returns |
| Dimension Tables | Customers, Products, Product Categories, Product Subcategories, Territories, Calendar |

---

## Data Preparation

Data preparation activities included:

- Data Profiling
- Data Quality Assessment
- Referential Integrity Validation
- Duplicate Validation
- Data Type Validation
- Relationship Validation
- Transformation Design
- Power Query Implementation

### Data Quality Validation

Validated:

- Foreign Key Integrity
- Primary Key Uniqueness
- Data Types
- Missing Values
- Duplicate Records
- Relationship Consistency

---

## Data Model

### Adventure Works Dimensional Model

<img width="657" height="743" alt="Screenshot 2026-06-19 220400" src="https://github.com/user-attachments/assets/15dea035-f4b3-4b75-87e8-cca738edd2d0" />

The model combines star-schema principles with a snowflake structure in the product hierarchy:

- Sales and Returns serve as fact tables.
- Product hierarchy is normalized into Products → Subcategories → Categories.
- Customers, Territories, and Calendar provide analytical context.

---

## Assumptions & Constraints

| ID | Assumption / Constraint |
|----|-------------------------|
| AC-01 | Dataset contains partial 2017 data (H1 only) |
| AC-02 | Returns table does not contain CustomerKey |
| AC-03 | Returns do not include return reasons |
| AC-04 | Discount information unavailable |
| AC-05 | Revenue derived from ProductPrice × OrderQuantity |
| AC-06 | Cost derived from ProductCost × OrderQuantity |
| AC-07 | Profit calculated as Revenue − Cost |
| AC-08 | Profit Margin derived from Profit and Revenue |
| AC-09 | OrderNumber does not support basket analysis |
| AC-10 | Customer segmentation limited to available attributes |

---

## Dashboard Solution

A two-page dashboard was developed to support executive monitoring and business investigation.

### Page 1 — Executive Performance Dashboard

**Objective:**

Provide a high-level view of growth, profitability, and revenue quality.

**Key Components:**

- Profit KPI
- Profit Margin KPI
- Revenue Growth KPI
- Revenue Trend Analysis
- Orders & AOV Analysis
- Revenue Contribution Analysis
- Mix Shift Analysis
- Revenue, Cost & Profit Trend Analysis
- Profitability Decomposition

<img width="1372" height="617" alt="Screenshot 2026-06-19 000852" src="https://github.com/user-attachments/assets/8b99a24e-04f5-408e-b3c2-a3447a8cdd54" />

---

### Page 2 — Business Drivers Dashboard

**Objective:**

Identify root causes behind business performance.

**Key Components:**

- Returns Analysis
- Product Profitability Analysis
- Customer Segment Analysis
- Regional Performance Analysis
- Revenue vs Return Risk Analysis
- Margin Analysis

<img width="1162" height="712" alt="Screenshot 2026-06-19 000955" src="https://github.com/user-attachments/assets/65570d4f-a1fb-424f-a54f-5e764c5fd896" />

---

## DAX Measures Developed

| Foundational Measures | Derived Measures | Advanced Measures |
|----------------------|------------------|-------------------|
| Revenue | Profit | Profit Margin % |
| Cost | AOV | Revenue Contribution % |
| Orders | ASP | Mix Shift |
| Units Sold | ARPC | Revenue Growth % |
| Return Quantity | Return Value | — |
| Customer Count | Net Revenue | — |
| — | Return Rate % | — |

---

## Key Insights

### 1. Revenue Growth Remains Strong

- Revenue Growth reached **211.07%**, indicating substantial commercial expansion.
- Growth appears primarily driven by increased commercial activity rather than significant increases in Average Order Value.

### 2. Revenue Concentration Risk

- The Bikes category contributes approximately **95% of category revenue**.
- This creates a significant dependency on a single product category.

### 3. Profitability Remains Healthy

- Profit Margin remains near **42%**, suggesting growth is generally translating into value creation.

### 4. Return-Related Revenue Leakage

- The Bikes category exhibits the highest return rates among major categories.
- Reducing returns represents a direct profitability improvement opportunity.

### 5. Regional Performance Is Concentrated

- Australia consistently generates the highest revenue and profit.
- This indicates both strong performance and concentration risk.

### 6. Margin Quality Differs Across Categories

- Accessories generate stronger margins than several higher-revenue categories.
- Revenue scale and profitability quality are not always aligned.

---

## Strategic Recommendations

### 1. Revenue Growth

Diversify growth beyond Bikes to reduce category concentration risk.

### 2. Profitability Improvement

Review high-revenue, low-profit products for pricing, cost, and portfolio optimization opportunities.

### 3. Returns Reduction

Prioritize return reduction initiatives within the Bikes category.

### 4. Regional Strategy

Replicate successful commercial practices from Australia across lower-performing territories.

### 5. Product Strategy

Increase focus on higher-margin products and cross-selling opportunities.

---

## Business Impact Framework

| Finding | Recommendation | Expected Business Impact |
|----------|---------------|--------------------------|
| Revenue concentrated in Bikes | Diversify category growth | Lower revenue concentration risk |
| High Bike return rate | Return reduction program | Higher Net Revenue |
| Strong Australian performance | Replicate best practices | Regional growth improvement |
| Margin variation across categories | Product mix optimization | Higher Profit Margin |
| High-revenue low-profit products | Profitability review | Improved profit generation |

---

## Tools Used

- Power BI
- Power Query
- DAX
- SQL
- BigQuery
- Excel

---

## Skills Demonstrated

### Business & Analytics

- Business Understanding
- Stakeholder Analysis
- KPI Design
- Business Question Development
- Insight Generation
- Recommendation Development

### Data

- Data Profiling
- Data Quality Assessment
- Data Modeling
- Relationship Design
- Data Validation

### Power BI

- Power Query
- DAX Development
- Dashboard Design
- Interactive Reporting
- Performance Analysis

### Communication

- Executive Reporting
- Data Storytelling
- Decision Support Analytics

---

## Repository Structure

```text
Adventure-Works-Profitability-Analytics/
├── README.md
├── Business/
│   ├── Business_Requirements_Document.pdf
│   ├── Business_Decisions_Framework.md
│   └── KPI_Framework.md
├── Data/
│   ├── Data_Model.png
│   └── Data_Model_Documentation.md
├── Dashboard/
│   ├── Dashboard_Page_1.png
│   └── Dashboard_Page_2.png
├── Insights/
│   └── Executive_Insights_Report.md
└── Case_Study/
    └── Adventure_Works_Case_Study.pdf
```

---

## Project Outcome

This project demonstrates an end-to-end analytics workflow covering:

- Business Understanding
- KPI Design
- Data Modeling
- Data Preparation
- DAX Development
- Dashboard Development
- Insight Generation
- Business Recommendation Formulation

The final solution enables stakeholders to move from performance monitoring to actionable decision-making through structured profitability and commercial performance analysis.
