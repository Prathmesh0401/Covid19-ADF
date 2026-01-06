# Data Model Design

## 1. Overview
This document describes the logical and physical data models used in the COVID-19 data engineering platform.  
The data model is designed to support **analytics workloads**, **BI consumption**, and **ad-hoc querying** while ensuring data quality and consistency.

---

## 2. Modeling Principles
The following principles guided the data model design:
- Read-optimized schemas for analytics
- Clear separation between raw, processed, and curated data
- Minimal transformations in the serving layer
- Schema evolution tolerance
- Deterministic and reproducible datasets

---

## 3. Data Layers

### 3.1 Raw Layer
- Stores source-aligned data
- No schema enforcement
- Immutable and append-only
- Used for replay and auditing

**Example entities:**
- `ecdc_cases_raw`
- `hospital_admission_raw`
- `population_raw`

---

### 3.2 Processed Layer
- Cleaned and standardized datasets
- Schema normalization
- Data type corrections
- Null handling and validation

**Example entities:**
- `cases_and_deaths_processed`
- `hospital_admission_processed`
- `population_processed`

---

### 3.3 Curated Layer
- Analytics-ready datasets
- Business-friendly schemas
- Loaded into Azure SQL Database
- Used by BI and reporting tools

**Example entities:**
- `covid_cases_daily`
- `covid_cases_by_country`
- `hospital_admission_summary`

---

## 4. Key Tables (Curated Layer)

### 4.1 `covid_cases_daily`
| Column Name | Data Type | Description |
|------------|----------|-------------|
| report_date | DATE | Reporting date |
| country | VARCHAR | Country name |
| country_code | VARCHAR | ISO country code |
| total_cases | BIGINT | Total cases |
| total_deaths | BIGINT | Total deaths |
| population | BIGINT | Population |

---

### 4.2 `hospital_admission_summary`
| Column Name | Data Type | Description |
|------------|----------|-------------|
| report_date | DATE | Reporting date |
| country | VARCHAR | Country |
| icu_admissions | BIGINT | ICU admissions |
| hospital_admissions | BIGINT | Total hospital admissions |

---

## 5. Keys & Indexing
- Composite keys used for date + country
- Clustered indexes on reporting date
- Non-clustered indexes for country-based filters

---

## 6. Data Quality Controls
- Schema validation in processed layer
- Row count checks between layers
- Null and negative value checks
- Referential consistency across datasets

---

## 7. Schema Evolution Strategy
- Backward-compatible schema changes
- New columns added with defaults
- Raw layer retained for full reprocessing if needed

---

## 8. Future Improvements
- Slowly Changing Dimensions (SCD Type 2)
- Data versioning
- Automated data quality metrics
