# 📊 Strategic Sales Report

---
## 🖼️ Dashboard & Chart Previews
Due to its vertical length, the full dashboard is best viewed directly. Click the links below to see the high-resolution images:

* **[View Full Dashboard](https://github.com/Heet-Jamariya/Strategic_Sales_Report/blob/main/screenshots/dashboard-full-view.jpg)**
* **[Filter Panel Details](https://github.com/Heet-Jamariya/Strategic_Sales_Report/blob/main/screenshots/dashboard-filters.png)**
* **[Revenue by Industry Chart](https://github.com/Heet-Jamariya/Strategic_Sales_Report/blob/main/screenshots/chart-treemap-industries.png)**
* **[US Sales Revenue Map](https://github.com/Heet-Jamariya/Strategic_Sales_Report/blob/main/screenshots/chart-geo-map.png)**

---

### 📝 Full Project Case Study
For a detailed, step-by-step breakdown of the project lifecycle—from initial requirements to final recommendations—please view the full case study.

➡️ [**Read the Full Case Study Here**](https://github.com/Heet-Jamariya/Strategic_Sales_Report/blob/main/CASE_STUDY.md)

---

## 📖 Project Overview
The primary objective of this project was to develop a comprehensive analytics dashboard in **Apache Superset** for an auction business. This dashboard replaces slow, manual reporting with a dynamic, self-service tool that allows stakeholders to track revenue, analyze sales trends, and identify key business drivers in real-time to make data-driven decisions.

The layout features Key Performance Indicator (KPI) cards for a high-level summary, a grid of ten specialized charts for detailed analysis, and an interactive filter panel.

---

## 💡 Key Insights & Recommendations

#### Key Insights:
* The **Manufacturing / Production** sector is the most significant revenue driver.
* Geographically, **California** is the highest-grossing state for sales.
* A high volume of sales occurs at lower price points (0-100 range), indicating a healthy market for smaller items.
* Analysis of unsold items shows which industries have the most capital tied up in inventory.

#### Strategic Recommendations:
1.  **Focus on High-Value Segments:** Double down on the Manufacturing sector by creating targeted marketing campaigns for industrial equipment, especially for potential buyers in California.
2.  **Optimize Low-Value Inventory:** Implement bundled deals or promotions for the high volume of lower-priced items to increase sell-through rates and reduce inventory costs.

---

## 📊 Dashboard Features

#### Key Performance Indicators Tracked:
* Total Lots Sold
* Total Revenue
* Average Starting Price & Sold Price
* % Above Starting Price
* Average High Estimate
* Unsold Lots & Their Starting Price

#### Key Visualizations & Analyses:
* **Geographic Analysis:** A map visualizing total sales revenue by US state.
* **Industry Segmentation:** A treemap breaking down total revenue by industry.
* **Time-Series Trend Analysis:** Line charts tracking sales volume and revenue over time.
* **Price Point Analysis:** A histogram showing the distribution of sales across different price brackets.
* **Pricing Strategy Evaluation:** A dual-axis chart comparing starting prices vs. final sold amounts.

---

## 🔧 Technical Highlights & Problem-Solving
This project involved overcoming several technical hurdles that required creative solutions:

* **Ensuring Accurate and Intuitive KPI Formatting:**
    * **Problem:** A critical KPI, "% Above Starting Price", was correctly calculated but displayed as a raw number instead of an intuitive percentage.
    * **Solution:** First, the SQL query was modified to calculate the pure decimal ratio. Second, Superset's built-in D3 Number Formatting (`.2%`) was applied in the chart's customization panel to visually convert the ratio.

* **Complex Trend Analysis (The Dual-Axis Chart):**
    * **Problem:** A requirement was to compare "Starting Price" and "Sold Price" trends on the same chart, which a simple line chart couldn't handle effectively.
    * **Solution:** This was solved by using Superset's "Mixed Time-Series Chart," which allows for plotting two distinct metrics against a shared time axis.

* **Aggregating Data for Time-Series Analysis:**
    * **Problem:** The raw sales data was transactional and needed to be aggregated into monthly buckets for trend analysis.
    * **Solution:** I used the chart's built-in **Time Grain** setting and a `COUNT(DISTINCT ...)` metric to have Superset automatically handle the `GROUP BY` aggregation.

* **Multi-Layered Geospatial Visualization:**
    * **Problem:** The map component required the strict ISO 3166-2 format (e.g., "US-CA"), which was not available in the raw data.
    * **Solution:** I created a **Calculated Column** using the SQL expression `CONCAT('US-', state_state_short_code)` to generate the required format on the fly.

* **Advanced Custom Binning for Price Distribution:**
    * **Problem:** The business needed to see item distribution in fixed-width price intervals, but Superset's standard histogram could not create them.
    * **Solution:** I engineered the data at the source by adding a **Calculated Column** using a `CASE & END` SQL statement to pre-calculate the correct price bucket for every row.

---

## 💻 Technologies Used
* **Apache Superset:** For dashboard development and visualization.
* **SQL:** For creating calculated columns and complex data queries.
* **Formatting:** For custom KPI and chart formatting.
* **Figma:** Used for initial UI/UX mockups.

---

## 📂 Project Assets
This repository contains the showcase materials for the project.
* The `screenshots` directory contains the high-resolution images of the dashboard.
* The `README.md` file provides this detailed overview of the project.
* An optional dashboard export file can be included to share the configuration.