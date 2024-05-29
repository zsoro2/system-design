# Data warehouse


### What are Data Warehouses?

A data warehouse is a centralized repository that stores large amounts of structured data from multiple sources. It is designed for query and analysis rather than transaction processing. Data warehouses support business intelligence activities, such as reporting, data analysis, and data mining, providing valuable insights for decision-making.



### Data Extraction, Transformation, and Loading (ETL):

- **Extraction**: Data is collected from various source systems like transactional databases, CRM systems, and flat files.
- **Transformation**: The extracted data is cleansed, formatted, and transformed into a consistent structure.
- **Loading**: The transformed data is loaded into the data warehouse.


### Fact and Dimension Tables

**Fact Tables:**
- **Purpose:** Store measurable, quantitative data for analysis.
- **Content:** Contains foreign keys to dimension tables and metrics like sales amount and quantity sold.
- **Example:**

sales_fact_table

| sale_id | product_id | customer_id | store_id | date_id  | sales_amount | quantity_sold |
|---------|------------|-------------|----------|----------|--------------|---------------|
| 1       | 101        | 1001        | 201      | 20200101 | 150.00       | 2             |

**Dimension Tables:**
- **Purpose:** Provide context and descriptive information related to facts.
- **Content:** Contains primary keys and attributes like product name, customer location, and store region.
- **Examples:**

product_dimension_table

| product_id | product_name | category | price |
|------------|--------------|----------|-------|
| 101        | Widget A     | Gadgets  | 75.00 |


customer_dimension_table

| customer_id | customer_name | location       | age |
|-------------|---------------|----------------|-----|
| 1001        | John Doe      | New York       | 35  |


date_dimension_table

| date_id  | date       | month | quarter | year |
|----------|------------|-------|---------|------|
| 20200101 | 2020-01-01 | Jan   | Q1      | 2020 |


### Star, Snowflake, OLAP
- **Star Schema:** Simplifies queries by having a central fact table surrounded by dimension tables.
- **Snowflake Schema:** Normalizes dimension tables to reduce redundancy but can complicate queries.
- **OLAP (Online Analytical Processing):** Tools and techniques used to analyze data in the warehouse, often supporting complex queries and data aggregation.

