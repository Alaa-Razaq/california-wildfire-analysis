# 🔥 California Wildfire Trends & Impact Analysis (2013–2019)

---

## 📑 Table of Contents

1. [Project Overview](#project-overview)
2. [Business Problem](#business-problem)
3. [Objectives](#objectives)
4. [Dataset](#dataset)
5. [Methodology](#methodology)
6. [Data Cleaning & Preparation (SQL)](#data-cleaning--preparation-sql)
7. [SQL Workflow & Queries](#sql-workflow--queries)
8. [Tools Used](#tools-used)
9. [Dashboard Components](#dashboard-components)
10. [Key Insights](#key-insights)
11. [Business Recommendations](#business-recommendations)
12. [What I Learned](#what-i-learned)
13. [Project Link](#project-link)

---

## 📊 Project Overview

This project analyzes wildfire activity across California from 2013 to 2019. The goal is to identify trends over time, highlight high-risk counties, and evaluate the overall impact in terms of wildfire counts and acres burned. The workflow follows an end-to-end process: **SQL for data preparation** and **Tableau for visualization**.

---

## ❓ Business Problem

Wildfires have significant environmental and economic impacts in California. Understanding when and where wildfires occur most frequently can help identify high-risk areas and inform prevention strategies.

---

## 🎯 Objectives

* Analyze wildfire trends over time
* Identify counties with the highest wildfire frequency
* Evaluate total acres burned per year
* Provide insights for risk awareness and resource planning

---

## 📂 Dataset

**Source:** Public wildfire dataset (Kaggle / government data)
link: https://www.kaggle.com/datasets/ananthu017/california-wildfire-incidents-20132020<img width="468" height="57" alt="image" src="https://github.com/user-attachments/assets/2b172724-d897-4e4c-a589-8dc62a95e775" />


**Fields used:**

* Year (Archiveyear → renamed to Year)
* County
* Acres Burned
* Incident Name (used for counting fires)

---

## 🧠 Methodology

1. **Data Collection** – Obtained wildfire dataset from a public source
2. **Data Cleaning** – Used SQL (PostgreSQL) to clean and prepare the data
3. **Data Transformation** – Converted data types and structured fields for analysis
4. **Data Analysis** – Aggregated wildfire counts and acres burned by year and county
5. **Data Visualization** – Built an interactive dashboard in Tableau
6. **Insight Generation** – Identified trends, high-risk counties, and key patterns

---

## 🧹 Data Cleaning & Preparation (SQL)

Performed in PostgreSQL before visualization:

* Imported raw CSV into PostgreSQL
* Standardized column names (e.g., `archiveyear` → `year`)
* Removed rows with missing/invalid values
* Converted data types (e.g., `acresburned` → numeric)
* Validated duplicates and ensured correct granularity (fire × county)
* Aggregated data by **county** and **year** for analysis
* Exported clean tables to CSV for Tableau

---

## 🧠 SQL Workflow & Queries

### Create clean table

```sql
CREATE TABLE wildfire_clean AS
SELECT
  name,
  counties AS county,
  CAST(acresburned AS FLOAT) AS acres,
  archiveyear AS year
FROM wildfire_analysis
WHERE acresburned IS NOT NULL;
```

### Fires by county (ranking)

```sql
SELECT
  county,
  COUNT(name) AS fire_count
FROM wildfire_clean
GROUP BY county
ORDER BY fire_count DESC;
```

### Fires by year (trend)

```sql
SELECT
  year,
  COUNT(name) AS fire_count
FROM wildfire_clean
GROUP BY year
ORDER BY year;
```

### Total acres burned by year

```sql
SELECT
  year,
  SUM(acres) AS total_acres
FROM wildfire_clean
GROUP BY year
ORDER BY year;
```

### Top 10 counties (2016–2019)

```sql
SELECT
  county,
  COUNT(name) AS fire_count
FROM wildfire_clean
WHERE year BETWEEN 2016 AND 2019
GROUP BY county
ORDER BY fire_count DESC
LIMIT 10;
```

---

## 🛠️ Tools Used

* **PostgreSQL (SQL)** → Data cleaning, transformation, aggregation
* **Tableau** → Visualization & interactive dashboard
* **CSV** → Data storage between tools

---

## 📈 Dashboard Components
## 📊 Tableau Dashboard

[View Interactive Dashboard](https://10ay.online.tableau.com/t/kadem5-0ccf4fe8aa/views/AlaaRazaq/Dashboard12)

### 1. Wildfire Trend Over Time

Line chart showing number of fires per year

### 2. Wildfire Distribution Map

Map showing wildfire counts by county

### 3. Total Acres Burned

Area chart showing wildfire impact over time

### 4. Top 10 Counties

Bar chart highlighting highest wildfire counts

### 5. Interactive Filter

Year slider for dynamic exploration

---

## 🔍 Key Insights

* Wildfires peaked in **2017**, with the highest number of incidents and acres burned
* **Riverside County** recorded the highest wildfire count between 2016–2019
* A noticeable decline in wildfire activity occurred after 2018

---

## 💡 Business Recommendations

* Increase wildfire prevention efforts in high-risk counties such as Riverside
* Allocate more emergency resources during peak wildfire years
* Monitor environmental conditions that contributed to the 2017 spike

---





