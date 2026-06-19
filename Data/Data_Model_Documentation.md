# Data Modeling

# 1. Modeling Objective

The data model was designed to support profitability, revenue growth, and commercial performance analysis across products, customers, categories, and regions.

The model enables stakeholders to:

- Monitor Profit, Profit Margin %, and Revenue Growth %
- Analyze product, category, customer, and regional performance
- Investigate profitability drivers
- Evaluate return-related revenue leakage
- Support data-driven commercial decisions

The design prioritizes analytical flexibility, accurate KPI calculation, and intuitive drill-down analysis.

---

# 2. Schema Overview

### Schema Type

**Hybrid Schema (Star + Snowflake)**

The model follows star-schema principles around the fact tables while preserving the natural Product hierarchy through separate Product, Subcategory, and Category dimensions.

### Why This Design Was Selected

- Supports category and product-level analysis without duplicating hierarchy attributes
- Maintains clear business relationships
- Enables hierarchical drill-down reporting
- Reduces redundancy while preserving analytical flexibility

This approach balances simplicity for reporting with support for product hierarchy analysis.

---

# 3. Fact Tables

| Fact Table | Grain | Purpose |
|------------|--------|----------|
| Sales | One row per (OrderNumber + OrderLineItem) | Supports revenue, profitability, growth, and customer analysis |
| Returns | One row per (ReturnDate + TerritoryKey + ProductKey) | Supports return analysis across products, categories, and territories |

---

# 4. Dimension Tables

| Dimension Table | Purpose |
|-----------------|----------|
| Calendar | Time-based analysis, trends, growth, and seasonality |
| Customers | Customer segmentation and performance analysis |
| Products | Product-level analysis and profitability reporting |
| Product_Subcategories | Intermediate product hierarchy |
| Product_Categories | Category-level analysis and contribution reporting |
| Territories | Regional performance and profitability analysis |

---

# 5. Relationship Design

### Relationship Strategy

The model follows a dimensional design where business events (Sales and Returns) are connected to descriptive dimensions.

### Cardinality

All relationships use a **One-to-Many (1:M)** structure:

```text
Dimension → Fact
```

### Filter Flow

All relationships use **single-direction filtering** from dimensions to fact tables.

This approach was selected to:

- Prevent ambiguous filter paths
- Improve model performance
- Simplify DAX calculations
- Ensure predictable aggregation behavior

### Shared Dimensions

Calendar, Product, and Territory are shared across Sales and Returns, enabling consistent reporting across both business processes.

---

# 6. Key Modeling Decisions

## Sales Grain Validation

Sales was modeled at the line-item level:

```text
(OrderNumber + OrderLineItem)
```

rather than at the order level.

This preserves product-level detail while supporting accurate revenue and profitability analysis.

A key implication is that order-level metrics such as AOV must be calculated using order aggregation rather than row counts.

---

## Product Hierarchy Preservation

The Product → Subcategory → Category hierarchy was retained instead of being flattened.

This supports:

- Category contribution analysis
- Mix shift analysis
- Hierarchical drill-down reporting

---

## Separate Sales and Returns Facts

Sales and Returns were modeled as independent fact tables because they represent different business events with different grains.

This preserves business meaning and prevents aggregation conflicts.

---

## Dedicated Calendar Dimension

A dedicated Calendar dimension was implemented to support:

- Trend analysis
- Revenue Growth calculations
- Seasonality analysis
- Consistent time intelligence

---

# 7. Modeling Assumptions & Constraints

| Assumption / Constraint | Business Impact |
|-------------------------|-----------------|
| Sales grain is (OrderNumber + OrderLineItem) | Prevents incorrect order-level calculations |
| Returns contain no CustomerKey | Customer-level return analysis is not possible |
| Revenue is derived using ProductPrice × OrderQuantity | Revenue depends on catalog pricing data |
| Cost is derived using ProductCost × OrderQuantity | Profitability depends on recorded product costs |
| Profit is derived as Revenue − Cost | Profit is not stored directly |
| Dataset covers Jan 2015 – Jun 2017 only | Full-year 2017 comparisons are invalid |
| Product hierarchy drives category reporting | Category analysis depends on hierarchy relationships |

---

### Business Value

The model provides the foundation for accurate profitability analysis, growth analysis, return analysis, and stakeholder-driven investigation workflows across products, customers, categories, and regions.
