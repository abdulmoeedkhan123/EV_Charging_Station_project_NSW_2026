# EV Charging Infrastructure Analytics Platform (NSW)

An end-to-end data engineering and analytics project built on the Databricks Lakehouse Platform using Medallion Architecture.

The project ingests raw EV charging infrastructure data, performs ETL transformations using PySpark, builds Gold-layer analytical datasets, and visualises business insights through interactive Databricks dashboards.

Raw Data
   ↓
Bronze Layer
   ↓
Silver Layer (Cleaning + Standardization)
   ↓
Gold Layer (Aggregations + KPIs)
   ↓
Databricks SQL Datasets
   ↓
Interactive Dashboard


# Medallion Architecture Section
1. Bronze Layer
workspace. default.ev_raw_data
2. Silver Layer
workspace. default.EV_Cleaned_Data
3. Gold Layer
gold_operator_performance
gold_capacity_per_station
gold_council_summary
gold_charger_type_summary

# ETL Workflow
Extraction
df = spark.table("workspace.default.ev_raw_data")

Transformation

1. Data Cleaning
2. Removed unnecessary columns
3. Dropped null records
4. Standardised schema
5. Feature Engineering
6. Created Location struct
7. Calculated Total Capacity(kW)
8. Converted plug counts to an integer
9. Data Standardisation
10. Renamed columns
11. Removed "kW" suffix
12. Casted data types
 df.write.mode("overwrite").saveAsTable("workspace.default.EV_Cleaned_Data")

Data Quality Checks
Checks performed:

1. Null value analysis
2. Row/column consistency checks
3. Datatype validation
4. Capacity transformation verification
null_counts = df.select([
    spark_sum(when(col(c).isNull(), 1).otherwise(0)).alias(c)
    for c in df.columns
])

| Gold Table                | Purpose                             |
| ------------------------- | ----------------------------------- |
| gold_capacity_per_station | station capacity analysis           |
| gold_operator_performance | operator comparison                 |
| gold_council_summary      | geographic infrastructure analytics |
| gold_charger_type_summary | AC vs DC insights                   |



# Business Insights
Key Insights
1. DC chargers are concentrated among a small number of operators
2. Certain councils have significantly lower EV infrastructure density
3. High-capacity stations are clustered in metropolitan areas
4. AC chargers dominate the total station count
5. Capacity distribution is uneven across postcodes

## Tech Stack

1. Databricks Lakehouse Platform
2. PySpark
3. Spark SQL
4. Delta Tables
5. Unity Catalogue
6. Medallion Architecture
7. Databricks SQL
8. Databricks Dashboards
9. Python

# Skills Demonstrated

1. Data Engineering
2. ETL Pipeline Development
3. PySpark Transformations
4. Data Cleaning
5. Data Modelling
6. Medallion Architecture
7. SQL Aggregations
8. Dashboard Development
9. Data Visualisation
10. Business Analytics
