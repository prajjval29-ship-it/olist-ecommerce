# Olist E-Commerce Data Engineering Project

An end-to-end Data Engineering project built using **Databricks, PySpark, Spark SQL, Delta Lake, and Python**. This project transforms the Brazilian Olist E-Commerce dataset into structured analytical layers and business-focused insights.
# Dashboards
https://dbc-3cd95548-ca94.cloud.databricks.com/dashboardsv3/01f1e6a2a6151829a2f00fe4a83af463/published?o=7474651605650608
## Architecture
<img width="487" height="269" alt="image" src="https://github.com/user-attachments/assets/41ee2eaa-fdb7-4eb9-93c7-d1a2ae52893a" />


The pipeline follows the **Medallion Architecture**:

- **Bronze:** Raw data ingestion and storage in Delta tables.
- **Silver:** Data cleaning, schema handling, standardization, quality checks, and transformations.
- **Gold:** Business-oriented analytical tables designed for reporting and insights.

## Technology Stack

| Technology | Purpose |
|---|---|
| Databricks Free Edition | Data engineering environment |
| Python | Programming and transformations |
| PySpark | Distributed data processing |
| Spark SQL | Analytical transformations and validation |
| Delta Lake | Reliable storage and table management |
| Unity Catalog | Data organization and governance |
| Git & GitHub | Version control and project management |
| Databricks AI/BI | Interactive dashboard |

## Dataset

The project uses the publicly available **Brazilian E-Commerce Public Dataset by Olist**.

Dataset source: [Olist Brazilian E-Commerce Dataset – Kaggle](https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce)

Five datasets were used:

- Orders
- Order Items
- Products
- Customers
- Sellers

The project does not ingest payments, reviews, geolocation, or category translation datasets.

## Project Structure

```text
olist-ecommerce/
│
├── 01_Notebooks/
│   ├── 01_bronze_ingestion
│   ├── 02_silver_transformations
│   ├── 03_gold_analytics
│   └── 04_validation_optimization_sql
│
├── 02_Dashboards/
│   └── Olist E-Commerce Analytics.lvdash.json
│
├── 03_Documentation/
│   ├── dashboard_insights.txt
│   └── olist_project_architecture.png
│
└── 04_Backup/
    └── olist_full_backup
```

## Data Engineering Implementation

### 1. Bronze Layer – Ingestion

- Loaded the five source datasets into Databricks.
- Performed initial schema inspection and data profiling.
- Stored ingested data in Delta tables.

### 2. Silver Layer – Transformation

- Handled missing values and schema inconsistencies.
- Renamed inconsistent column names.
- Applied data quality checks.
- Standardized data types and prepared datasets for analytical joins.
- Preserved appropriate business keys and table grains.

### 3. Gold Layer – Analytics

Created eight Gold analytical tables:

1. `monthly_orders`
2. `golden_order_summary`
3. `gold_order_analytics`
4. `gold_product_analytics`
5. `gold_category_performance`
6. `gold_customer_analytics`
7. `gold_seller_analytics`
8. `gold_seller_state_performance`

These tables support order, product, category, customer, and seller analysis.

### 4. Validation and Optimization

Implemented and explored:

- Primary-key and uniqueness validation.
- Null and duplicate checks.
- Row-count reconciliation across layers.
- Gold and Silver financial metric reconciliation.
- Spark SQL transformations and comparisons.
- Broadcast joins and query-plan analysis.
- Repartitioning and coalescing.
- Caching and predicate pushdown.
- Data skew analysis and a salting demonstration.

### 5. Incremental Processing Demonstration

Implemented a separate Delta Lake MERGE-based incremental processing demonstration.

- Tested initial and incoming batches.
- Demonstrated inserts and updates.
- Tested idempotent reruns.
- Kept the demonstration isolated from the main analytical pipeline.

**Note:** This is a demonstration using a static historical dataset, not a production CDC implementation.

## Dashboard – Olist E-Commerce Analytics

Created an interactive Databricks AI/BI dashboard with two pages and 17 visualizations.

**Page 1 – Executive Overview**
- Total orders and delivered orders.
- Revenue, freight, total order value and average order value.
- Average delivery time.
- Monthly order trends.
- Order status distribution.
- On-time versus late deliveries.

**Page 2 – Product, Customer & Seller Insights**
- Top categories by revenue and units sold.
- Average selling price by category.
- Top customers by spending.
- One-time versus repeat customers.
- Top sellers by revenue.
- Revenue by seller state.

## Selected Project Findings

- **99,441** total orders.
- **96,478** delivered orders.
- **112,650** order items.
- **32,951** products.
- **3,095** sellers.
- **96,096** unique customers.
- **R$13.59 million** in product revenue, excluding freight.
- **R$15.84 million** in total order value, including freight.
- Approximately **8.11%** late deliveries among delivered orders with an available actual delivery date.

### Important Metric Definitions

- Product revenue excludes freight.
- Total order value includes freight.
- Average order value includes freight.
- Eight delivered orders without an actual delivery date are excluded from the delivery-performance classification.
- 775 orders have no matching order-item data in the source join.

## Documentation

The `03_Documentation/` folder contains:
- `dashboard_insights.txt` – Detailed analysis, metric definitions, findings, and recommendations.
- `olist_project_architecture.png` – End-to-end project architecture.

## How to Explore the Project

1. Clone this repository.
2. Download the Olist public dataset from Kaggle.
3. Create or configure a Databricks workspace with Unity Catalog access.
4. Upload the required source CSV files to the expected Unity Catalog Volume location:
   `/Volumes/workspace/default/olist_raw/raw_data/`
5. Import the notebooks from `01_Notebooks/` into Databricks.
6. Execute the notebooks in the intended order:
   - Bronze ingestion
   - Silver transformations
   - Gold analytics
   - Validation, optimization and SQL
7. Explore the resulting Delta tables and dashboard definition.

The notebooks use the catalog and schema `workspace.olist`. Adjust the volume, catalog, and schema references if your environment differs.

## Author

**Prajjval**

