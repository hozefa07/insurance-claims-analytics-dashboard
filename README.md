# Insurance Claims Analytics Dashboard

## 📊 Project Overview

This project provides a comprehensive analytics solution for insurance claims data, featuring end-to-end data processing pipelines and an interactive AI/BI dashboard for executive and regulatory reporting.

**Live Dashboard**: [View Published Dashboard](https://dbc-9d973e8e-1326.cloud.databricks.com/dashboardsv3/01f17546a5a419eabe7f46753a3a26ce/published?o=7474657087609619)

## 🎯 Key Features

### Interactive Dashboard
- **Executive Insights**: 5 crucial analytical observations derived from claims patterns
- **KPI Counters**: Total claims (104,706), total amount (HKD 608.6M), average claim (HKD 5,813)
- **Colorful Visualizations**: 
  - Claims by Channel (Agency, Bank, Broker, Direct, Group Scheme, Online)
  - Geographic Distribution (10 Asia-Pacific countries)
  - Claim Type Analysis (7 categories: Periodic Payment, Death Claim, IBNR, etc.)
  - Monthly Trend Analysis (2026 data)
- **Regulatory Pivot Table**: Benefit Level 1/2 vs Claim Types cross-tabulation

### Data Pipeline
- **Gold-layer KPI tables** built from cleansed Silver layer data
- **6 analytical tables** covering benefits, channels, geography, claim types, and temporal trends
- **Databricks SQL-based** transformations for scalability

## 📂 Repository Structure

```
├── README.md                          # This file
├── 03_Gold_KPI_Build.py              # Main notebook with all gold-layer table creation
├── DASHBOARD_SCHEMA.md               # Dashboard structure and dataset documentation
└── LICENSE                           # MIT License
```

## 🗃️ Data Architecture

### Gold Layer Tables (2026 Claims Data)

All tables are created in catalog `claims_data_analysis.claims_db`:

1. **gold_kpi_summary_2026** - Overall portfolio metrics
2. **gold_benefit_summary_2026** - Claims by benefit category (Level 1/2)
3. **gold_channel_summary_2026** - Claims by distribution channel
4. **gold_geography_summary_2026** - Claims by country (Asia-Pacific)
5. **gold_sun_summary_2026** - Claims by SUN claim type classification
6. **gold_monthly_summary_2026** - Time-series analysis by accounting period

### Source Data
- **Silver layer table**: `claims_data_analysis.claims_db.claims_silver_2026`
- **Schema**: 26 columns including policy info, amounts, dates, benefit/channel/geography codes and enriched descriptions

## 🚀 Getting Started

### Prerequisites
- Databricks workspace with access to Unity Catalog
- SQL Warehouse for query execution
- Access to the source `claims_silver_2026` table

### Running the Pipeline

1. **Import the notebook** into your Databricks workspace
2. **Attach to a SQL Warehouse** (no cluster needed)
3. **Run all cells** to create the 6 gold-layer tables
4. **Verify execution** using the validation cells included in the notebook

### Creating Your Own Dashboard

1. Navigate to **Dashboards** in Databricks
2. Create a new dashboard
3. Add datasets pointing to the gold-layer tables
4. Build visualizations using the provided schemas

## 📈 Key Insights from the Data

Based on the 2026 claims analysis (104,706 claims totaling HKD 608.6M):

### 1. Claims Concentration Risk
- Linked Long Term products show significant exposure clustering
- Periodic Payment claims dominate volume (53.7% of all claims)
- Reserve adequacy review recommended

### 2. Channel Efficiency Disparity
- **Agency** leads with 40.0% of claims (41,926 claims, HKD 241.9M)
- **Bank** channel: 25.0% share (26,225 claims, HKD 151.9M)
- **Broker**: 15.2% (15,876 claims, HKD 92.8M)
- **Direct/Online/Group Scheme**: Combined 19.8%

### 3. Geographic Concentration
- **Hong Kong** dominates: 20.2% of claims (21,136), HKD 122.7M
- **Indonesia**: 14.8% (15,541 claims), HKD 92.3M
- **Malaysia**: 13.9% (14,503 claims), HKD 84.8M
- Southeast Asian markets show diverse patterns

### 4. Claim Type Distribution
- **Periodic Payment**: 56,214 claims (53.7%)
- **Bonus/Interest Allocation**: 16,784 claims (16.0%)
- **Annuity Payment**: 13,561 claims (13.0%)
- **Surrender**: 9,075 claims (8.7%)
- **Maturity**: 4,548 claims (4.3%)
- **Death Claim**: 3,343 claims (3.2%)
- **IBNR**: 1,181 claims (1.1%)

### 5. Temporal Patterns
- Monthly claim volume ranges from 7,030 to 9,806 claims
- Average claim amounts vary from HKD 5,096 (January) to HKD 6,476 (December)
- No strict seasonal pattern; suggests operational factors at play

## 🛠️ Technical Stack

- **Platform**: Databricks Lakehouse
- **Query Engine**: SQL (Spark SQL)
- **Catalog**: Unity Catalog
- **Dashboard**: Databricks AI/BI Dashboard (Genie)
- **Language**: SQL
- **Data Format**: Delta Lake tables

## 📊 Dashboard Theme

The dashboard features a modern, executive-ready design:
- **12-color vibrant palette** for chart series
- **Inter font** for professional typography
- **Responsive layout** with proper spacing and shadows
- **Light mode optimized** with good contrast

## 🔍 Data Quality Notes

- **104,706 claims** across 2026 accounting periods
- **10 countries** in Asia-Pacific region
- **6 distribution channels** tracked
- **30 distinct benefit codes** and **17 SUN claim codes**
- Data includes both positive payouts and negative adjustments (min: -HKD 173,324)

## 📝 License

This project is licensed under the MIT License - see LICENSE file for details.

## 🤝 Contributing

Contributions, issues, and feature requests are welcome!

## 👤 Author

**Hozefa Sunwari**
- Email: hozefasunwari.52@gmail.com
- Databricks Workspace: `claims_data_analysis`

## 🙏 Acknowledgments

- Built using Databricks AI/BI Dashboard capabilities
- Powered by Unity Catalog for data governance
- Designed for insurance regulatory reporting standards

---

**Note**: The published dashboard URL provides interactive access to all visualizations and supports filtering and drill-down capabilities. No Databricks authentication required for viewers (shared data permission mode).