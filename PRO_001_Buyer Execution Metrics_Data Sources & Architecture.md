# End-to-End ETL & Power BI Reporting Process

## 1. Source System: SAP
- **Source**: SAP ERP (transactional and master data)
- **Extraction type**: Incremental (posting date / change date)
- **Goal**: Provide reliable, auditable source data for analytics

---

## 2. Data Ingestion: Talend → Amazon S3
- **Tool**: Talend
- **Process**:
  - Extract data from SAP
  - Apply minimal validation and formatting
  - Load flat files (CSV / Parquet) into **Amazon S3**
- **Design principle**:  
  - No business logic at this stage  
  - Preserve source fidelity

---

## 3. Landing Layer: Snowflake (Snowpipe)
- **Tool**: Snowpipe
- **Process**:
  - Automatically ingest files from S3
  - Load data into **temporary / landing tables**
- **Purpose**:
  - Raw data preservation
  - Load traceability (file name, load timestamp)
  - Reprocessing and troubleshooting

---

## 4. Conformed Layer: Standardized SAP Tables
- **Process**:
  - Flatten SAP structures
  - Standardize column names, data types, and keys
  - Deduplicate and filter invalid records
- **Output**:
  - Clean, reusable **conformed tables**
- **Goal**:
  - Establish a single, consistent SAP data foundation

---

## 5. Business Transformation Layer: SAP Analytics Schema
- **Logic applied**:
  - Business rules and calculations
  - Status mapping and derived fields
  - Snapshot and historical logic
- **Output**:
  - Dedicated **SAP analytics schema** in Snowflake
- **Reason for separation**:
  - Isolate business logic
  - Improve maintainability and reuse
  - Protect upstream layers

---

## 6. Reporting Views for Power BI

### 6.1 13-Week Historical Summary Views
- Weekly snapshot–based aggregations
- Optimized for trend and KPI analysis
- Reduced row volume for performance

### 6.2 Current-Week Detail Views
- Transaction-level detail
- Near–real-time visibility
- Supports drill-through and root-cause analysis

---

## 7. Power BI Data Consumption (Power Query)
- **Connection**: Import mode (SQL-based)
- **Power Query role**:
  - Consume Snowflake reporting views
  - Apply light shaping (rename, filter)
  - Avoid complex business logic
- **Best practice**:
  - Keep transformations in Snowflake

---

## 8. Power BI Data Model
- **Model type**: Star schema
- **Components**:
  - Fact tables (13-week summary, current-week detail)
  - Dimension tables (date, plant, material, vendor, etc.)
- **Optimizations**:
  - Minimal relationships
  - Bridge tables where required
  - Measures defined in DAX

---

## 9. Power BI Report Visualization
- **Report structure**:
  - Executive overview (13-week trends)
  - Operational dashboards (current-week details)
  - Drill-through and filtering paths
- **Design focus**:
  - Clear KPIs
  - Consistent metric definitions
  - Actionable insights for users

---

## 10. Report Subject Divide
- **Purchase Request (PR)** is the first step before creating a Purchase Order — it shows what materials or services are being requested but not yet ordered.
- **Past Due** means the PO should have been delivered already, but it’s still not received or closed.
- **Pushout PO** are orders that have been delayed to a later delivery date, usually to balance inventory or adjust to lower demand.
- **Cancel POs** are orders that are no longer needed and have been officially canceled before delivery.
- **Pull-in PO** are orders where buyers ask suppliers to deliver earlier than the original schedule.
- **E&O Reason Code** shows why certain materials became excess or obsolete, helping to identify and prevent waste.
