# Dashboard Schema Documentation

## Dashboard Structure

**Dashboard Name**: Insurance Claims Analytics Dashboard  
**Published URL**: https://dbc-9d973e8e-1326.cloud.databricks.com/dashboardsv3/01f17546a5a419eabe7f46753a3a26ce/published?o=7474657087609619

### Layout Overview

The dashboard is organized into a single-page executive view with the following sections:

1. **Executive Insights** (Row 0-5, Full Width)
2. **KPI Counters** (Row 6-9, 3 columns)
3. **Channel & Geography Charts** (Row 10-17, Side by side)
4. **Monthly Trend Line Chart** (Row 18-25, Full Width)
5. **Claim Types Bar Chart** (Row 26-33, Full Width)
6. **Regulatory Pivot Table** (Row 34-45, Full Width)

## Datasets

### 1. KPI Summary Dataset
**Dataset Name**: `datasets/kpi_summary`  
**Source Table**: `claims_data_analysis.claims_db.gold_kpi_summary_2026`  
**Purpose**: Overall portfolio metrics

**Columns**:
- `total_claim_rows` (integer) - Total number of claim records
- `total_claim_amount_hkd` (float) - Sum of all claim amounts in HKD
- `avg_claim_amount_hkd` (float) - Average claim amount
- `min_claim_amount_hkd` (float) - Minimum claim amount
- `max_claim_amount_hkd` (float) - Maximum claim amount
- `distinct_benefit_codes` (integer) - Count of unique benefit codes
- `distinct_sun_codes` (integer) - Count of unique SUN codes
- `distinct_channels` (integer) - Count of unique channels
- `distinct_geographies` (integer) - Count of unique geographies

**Sample Output**:
```
Total Claims: 104,706
Total Amount: HKD 608,637,673
Average Claim: HKD 5,813
```

### 2. Channel Summary Dataset
**Dataset Name**: `datasets/channel_summary`  
**Source Table**: `claims_data_analysis.claims_db.gold_channel_summary_2026`  
**Purpose**: Claims performance by distribution channel

**Columns**:
- `channel_code` (string) - Channel identifier (Agency, Bank, Broker, Direct, Group Scheme, Online)
- `channel_name` (string) - Human-readable channel name (currently null in data)
- `channel_description` (string) - Detailed channel description (currently null in data)
- `claim_count` (integer) - Number of claims for this channel
- `total_claim_amount_hkd` (float) - Total claim amount in HKD
- `avg_claim_amount_hkd` (float) - Average claim amount
- `min_claim_amount_hkd` (float) - Minimum claim amount
- `max_claim_amount_hkd` (float) - Maximum claim amount

**Sample Data**:
```
Agency: 41,926 claims, HKD 241.9M
Bank: 26,225 claims, HKD 151.9M
Broker: 15,876 claims, HKD 92.8M
```

### 3. Geography Summary Dataset
**Dataset Name**: `datasets/geography_summary`  
**Source Table**: `claims_data_analysis.claims_db.gold_geography_summary_2026`  
**Purpose**: Geographic distribution of claims

**Columns**:
- `geography_country` (string) - Country name
- `geography_weight` (integer) - Weight/priority for ranking
- `claim_count` (integer) - Number of claims
- `total_claim_amount_hkd` (float) - Total claim amount in HKD
- `avg_claim_amount_hkd` (float) - Average claim amount
- `min_claim_amount_hkd` (float) - Minimum claim amount
- `max_claim_amount_hkd` (float) - Maximum claim amount

**Countries Covered** (10 Asia-Pacific markets):
- Hong Kong (21,136 claims, HKD 122.7M)
- Indonesia (15,541 claims, HKD 92.3M)
- Malaysia (14,503 claims, HKD 84.8M)
- Singapore (12,472 claims, HKD 71.3M)
- Vietnam (10,568 claims, HKD 61.5M)
- Thailand (10,541 claims, HKD 60.3M)
- Philippines (10,433 claims, HKD 60.3M)
- Cambodia (4,174 claims, HKD 24.1M)
- Laos (3,236 claims, HKD 19.2M)
- Myanmar (2,102 claims, HKD 12.2M)

### 4. Monthly Summary Dataset
**Dataset Name**: `datasets/monthly_summary`  
**Source Table**: `claims_data_analysis.claims_db.gold_monthly_summary_2026`  
**Purpose**: Time-series analysis of claims by month

**Columns**:
- `ACCT_PERIOD` (integer) - Accounting period (format: YYYYMMM, e.g., 2026001 = January 2026)
- `claim_count` (integer) - Number of claims in the month
- `total_claim_amount_hkd` (float) - Total claim amount
- `avg_claim_amount_hkd` (float) - Average claim amount
- `min_claim_amount_hkd` (float) - Minimum claim amount
- `max_claim_amount_hkd` (float) - Maximum claim amount
- `distinct_policies` (integer) - Unique policies with claims
- `distinct_benefit_codes` (integer) - Unique benefit codes
- `distinct_sun_codes` (integer) - Unique SUN codes
- `distinct_channels` (integer) - Unique channels
- `distinct_geographies` (integer) - Unique geographies

**Sample Data** (12 months in 2026):
```
2026001 (Jan): 8,326 claims, HKD 42.4M
2026002 (Feb): 9,525 claims, HKD 49.7M
...
2026012 (Dec): 7,923 claims, HKD 51.3M
```

### 5. SUN Type Summary Dataset
**Dataset Name**: `datasets/sun_type_summary`  
**Source Table**: `claims_data_analysis.claims_db.gold_sun_summary_2026`  
**Purpose**: Claims breakdown by SUN claim type classification

**Columns**:
- `sun_code` (integer) - SUN classification code
- `sun_claim_type` (string) - Claim type category
- `sun_description` (string) - Detailed description
- `claim_count` (integer) - Number of claims
- `total_claim_amount_hkd` (float) - Total amount
- `avg_claim_amount_hkd` (float) - Average amount
- `min_claim_amount_hkd` (float) - Minimum amount
- `max_claim_amount_hkd` (float) - Maximum amount

**Claim Types** (7 categories):
1. **Periodic Payment** - 56,214 claims (53.7%)
2. **Bonus/Interest Allocation** - 16,784 claims (16.0%)
3. **Annuity Payment** - 13,561 claims (13.0%)
4. **Surrender** - 9,075 claims (8.7%)
5. **Maturity** - 4,548 claims (4.3%)
6. **Death Claim** - 3,343 claims (3.2%)
7. **IBNR** (Incurred But Not Reported) - 1,181 claims (1.1%)

### 6. Benefit vs Claim Type Matrix Dataset
**Dataset Name**: `datasets/benefit_claim_type_matrix`  
**Source Table**: Dynamic SQL query on `claims_silver_2026`  
**Purpose**: Cross-tabulation for regulatory pivot table

**Columns**:
- `benefit_level_1` (string) - Primary benefit category
- `benefit_level_2` (string) - Secondary benefit sub-category
- `sun_claim_type` (string) - Claim type
- `claim_count` (integer) - Count of claims for this combination
- `total_amount_hkd` (float) - Total amount
- `avg_amount_hkd` (float) - Average amount

**Example Combinations**:
```
Linked Long Term > A&H Accident & Disability > Death Claim: 93 claims
Linked Long Term > A&H Critical Illness > Periodic Payment: 1,480 claims
```

## Widget Specifications

### 1. Executive Insights Text Box
- **Type**: Markdown text widget
- **Position**: Row 0, Column 0, Width 12, Height 6
- **Content**: 5 key analytical insights for management

### 2. Total Claims Counter
- **Widget Type**: Counter
- **Position**: Row 6, Column 0, Width 4, Height 4
- **Dataset**: `datasets/kpi_summary`
- **Field**: `total_claim_rows`
- **Format**: Absolute number (104,706)

### 3. Total Amount Counter
- **Widget Type**: Counter
- **Position**: Row 6, Column 4, Width 4, Height 4
- **Dataset**: `datasets/kpi_summary`
- **Field**: `total_claim_amount_hkd`
- **Format**: Currency (HKD)

### 4. Average Amount Counter
- **Widget Type**: Counter
- **Position**: Row 6, Column 8, Width 4, Height 4
- **Dataset**: `datasets/kpi_summary`
- **Field**: `avg_claim_amount_hkd`
- **Format**: Currency (HKD)

### 5. Claims by Channel Bar Chart
- **Widget Type**: Bar chart (vertical)
- **Position**: Row 10, Column 0, Width 6, Height 8
- **Dataset**: `datasets/channel_summary`
- **X-axis**: `channel_code` (categorical)
- **Y-axis**: `claim_count` (quantitative)
- **Color**: `channel_code` (6 distinct colors)

### 6. Claims by Geography Bar Chart
- **Widget Type**: Bar chart (vertical)
- **Position**: Row 10, Column 6, Width 6, Height 8
- **Dataset**: `datasets/geography_summary`
- **X-axis**: `geography_country` (categorical)
- **Y-axis**: `claim_count` (quantitative)
- **Color**: `geography_country` (10 distinct colors)

### 7. Monthly Trend Line Chart
- **Widget Type**: Line chart
- **Position**: Row 18, Column 0, Width 12, Height 8
- **Dataset**: `datasets/monthly_summary`
- **X-axis**: `ACCT_PERIOD` (temporal)
- **Y-axis**: `claim_count` (quantitative)

### 8. Claims by Type Bar Chart
- **Widget Type**: Bar chart (horizontal)
- **Position**: Row 26, Column 0, Width 12, Height 8
- **Dataset**: `datasets/sun_type_summary`
- **X-axis**: `sun_claim_type` (categorical)
- **Y-axis**: `claim_count` (quantitative)
- **Color**: `sun_claim_type` (7 distinct colors)

### 9. Regulatory Pivot Table
- **Widget Type**: Pivot table
- **Position**: Row 34, Column 0, Width 12, Height 12
- **Dataset**: `datasets/benefit_claim_type_matrix`
- **Row Headers**: `benefit_level_1`, `benefit_level_2` (nested)
- **Column Headers**: `sun_claim_type`
- **Cell Values**: `claim_count` (formatted as plain number with compact abbreviation)

## Theme Configuration

### Color Palette (12 colors for visualizations)
1. #FF6B6B (Coral Red)
2. #4ECDC4 (Teal)
3. #45B7D1 (Sky Blue)
4. #FFA07A (Light Salmon)
5. #98D8C8 (Mint)
6. #F7DC6F (Golden Yellow)
7. #BB8FCE (Lavender)
8. #85C1E2 (Light Blue)
9. #F8B739 (Amber)
10. #52B788 (Green)
11. #E76F51 (Burnt Orange)
12. #2A9D8F (Deep Teal)

### Typography
- **Font Family**: Inter (open source, professional)
- **Widget Titles**: Bold, larger size
- **Body Text**: Regular weight

### Layout
- **Canvas Background**: Light grey (#F8F9FA)
- **Widget Background**: White (#FFFFFF)
- **Widget Corner Radius**: 8px
- **Widget Shadow**: 15% opacity
- **Widget Margin**: 12px
- **Widget Padding**: 16px

### Grid Styling
- **Grid Lines**: Light grey (#E8E8E8)
- **Axis Lines**: Medium grey (#CCCCCC)
- **Selection Color**: Teal accent (#2A9D8F)

## Data Refresh

All widgets refresh automatically when:
- Dashboard is opened
- User clicks refresh button
- Underlying tables are updated

**Note**: The dashboard uses "shared data permission" mode, meaning viewers see data using the dashboard owner's credentials. No individual authentication required for viewers.