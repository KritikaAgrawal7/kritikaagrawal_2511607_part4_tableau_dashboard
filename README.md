## Data Inspection & Assumptions

The dataset was successfully imported into Tableau and all fields were reviewed to verify their data types, roles, and completeness before creating visualizations.

### Data Type Verification

- **Order Date** and **Ship Date** were correctly recognized as **Date** fields.
- **Sales**, **Profit**, **Discount**, **Quantity**, **Delivery Days**, and **Customer Rating** were recognized as **numerical measures**.
- **Order ID** and **Customer ID** were treated as **dimensions** (unique identifiers).
- **Region**, **State**, **City**, **Category**, **Sub Category**, **Customer Segment**, **Ship Mode**, and **Campaign Channel** were recognized as **categorical dimensions**.
- **Return Flag** was identified as a **binary field** (0 = Not Returned, 1 = Returned).

### Missing Values

The following missing values were identified during data inspection:

| Column | Missing Values | Assumption |
|--------|---------------:|------------|
| Campaign Channel | 24 | Treated as unknown or unavailable campaign information. Records were retained for analysis. |
| Customer Rating | 32 | Represents customers who did not provide a rating. Records were retained as the remaining transaction data is valid. |

### Assumptions

- Blank values in **Campaign Channel** were assumed to represent unavailable or untracked marketing campaign information.
- Blank values in **Customer Rating** were assumed to indicate that customers did not submit a rating.
- Records containing missing values were retained because the missing information does not affect the validity of the corresponding sales transactions.
- No data type corrections were required after importing the dataset into Tableau.
- No additional data cleaning was performed, as the objective of this project is to inspect and analyze the provided dataset rather than modify it.

## Calculated Fields

### 1. Profit Margin
**Formula:**
```tableau
[Profit] / [Sales]
```

**Purpose:**
Calculates the percentage of sales retained as profit. It is used to evaluate profitability across regions, products, and customer segments.

---

### 2. Cost
**Formula:**
```tableau
[Sales] - [Profit]
```

**Purpose:**
Estimates the cost incurred for each sale by subtracting profit from sales. This helps compare revenue against underlying costs.

---

### 3. Average Order Value (AOV)
**Formula:**
```tableau
SUM([Sales]) / COUNTD([Order ID])
```

**Purpose:**
Measures the average revenue generated per order. This KPI helps evaluate customer purchasing behavior and the effectiveness of sales strategies.

---

### 4. Return Rate
**Formula:**
```tableau
SUM([Return Flag]) / COUNTD([Order ID])
```

**Purpose:**
Calculates the proportion of returned orders relative to total orders. It helps identify product quality or customer satisfaction issues.

---

### 5. Shipping Delay Bucket
**Formula:**
```tableau
IF [Delivery Days] <= 2 THEN
    "Fast (0-2 Days)"
ELSEIF [Delivery Days] <= 5 THEN
    "Standard (3-5 Days)"
ELSE
    "Delayed (6+ Days)"
END
```

**Purpose:**
Groups delivery times into meaningful business categories to simplify the analysis of shipping performance.

## Dashboard Overview

An executive sales dashboard was created in Tableau to provide an interactive overview of business performance for the 2024–2025 period.

### Dashboard Components

#### KPI Cards
The dashboard includes the following summary KPIs:

- Total Sales
- Total Profit
- Profit Margin

#### Visualizations

The dashboard contains the following analytical views:

1. **Sales Trend View** – Line chart showing monthly sales performance over time.
2. **Regional Performance View** – Horizontal bar chart comparing sales by state with profit represented using color intensity.
3. **Category Profitability View** – Horizontal bar chart comparing profit across categories and sub-categories.
4. **Customer Segment View** – Horizontal bar chart comparing sales across customer segments.
5. **Shipping Performance View** – Stacked bar chart showing sales by shipping mode and shipping delay bucket.
6. **Discount vs Profit View** – Scatter plot illustrating the relationship between discount and profit at the order level.
7. **Return Analysis View** – Horizontal bar chart showing returned orders by product category with return rate highlighted.

## Dashboard Interactivity

The dashboard supports interactive exploration through filters and filter actions.

### Interactive Filters

The following filters are available to users:

- Region
- Category
- Customer Segment
- Ship Mode

### Filter Action

The **Regional Performance View** has been configured as an interactive filter.

When a user selects a state from the Regional Sales & Profit Performance chart, all KPI cards and dashboard visualizations update automatically to display metrics only for the selected state. Clearing the selection restores the complete dashboard view.

This interaction enables executives to quickly analyze regional performance without navigating to separate reports.

## Key Design Decisions

- Appropriate chart types were selected based on the business question being answered.
- KPI cards provide an immediate summary of overall business performance.
- Consistent color encoding is used throughout the dashboard for readability.
- Interactive filters enable drill-down analysis.
- The dashboard uses a clean layout with minimal visual clutter to support executive decision-making.

