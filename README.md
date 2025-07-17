# 📊 Strategic Sales Report

![Strategic Sales Report Dashboard](https://github.com/Heet-Jamariya/Strategic_Sales_Report/blob/8a9722feb08d86e9e3ec87c6ae7f9e211bc4ddca/screenshots/dashboard-full-view.jpg)

---

## 📖 Project Overview
The primary objective of this project was to develop a comprehensive analytics dashboard in **Apache Superset** for an auction business. This dashboard replaces slow, manual reporting with a dynamic, self-service tool that allows stakeholders to track revenue, analyze sales trends, and identify key business drivers in real-time to make data-driven decisions.

The layout features Key Performance Indicator (KPI) cards for a high-level summary, a grid of ten specialized charts for detailed analysis, and an interactive filter panel.

---

## 💡 Key Insights & Recommendations
Based on the analysis, several key insights were uncovered:
* The **Manufacturing / Production** sector is the most significant revenue driver.
* Geographically, **California** is the highest-grossing state for sales.
* A high volume of sales occurs at lower price points (0-100 range), indicating a healthy market for smaller items.
* Analysis of unsold items shows which industries have the most capital tied up in inventory, presenting an opportunity for targeted promotions.

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
    * **Problem:** A critical KPI, "% Above Starting Price", was correctly calculated but displayed as a raw number (e.g., "79.87") instead of an intuitive percentage.
    * **Solution:** First, the SQL query was modified to calculate the pure decimal ratio (0.7987). Second, Superset's built-in D3 Number Formatting (`.2%`) was applied in the chart's customization panel to visually convert the ratio into a user-friendly percentage.

* **Complex Trend Analysis (The Dual-Axis Chart):**
    * **Problem:** A requirement was to compare "Starting Price" and "Sold Price" trends on the same chart, which a simple line chart couldn't handle effectively.
    * **Solution:** This was solved by using Superset's "Mixed Time-Series Chart." This allowed for plotting two distinct metrics against a shared time axis, creating an intuitive dual-line comparison.

* **Aggregating Data for Time-Series Analysis:**
    * **Problem:** The raw sales data was transactional and needed to be aggregated into monthly buckets for trend analysis.
    * **Solution:** Instead of writing a complex aggregation query, I used the chart's built-in **Time Grain** setting. By specifying "Month" as the grain and `COUNT(DISTINCT catalog_id)` as the metric, Superset automatically handled the `GROUP BY` aggregation.

* **Multi-Layered Geospatial Visualization:**
    * **Problem:** The map component required the strict ISO 3166-2 format (e.g., "US-CA"), which was not available in the raw data.
    * **Solution:** I created a **Calculated Column** directly within the Superset dataset. Using the SQL expression `CONCAT('US-', state_state_short_code)`, a new, properly formatted column was generated on the fly to solve the issue.

* **Advanced Custom Binning for Price Distribution:**
    * **Problem:** The business needed to see item distribution in fixed-width price intervals (e.g., buckets of $18,000), but Superset's standard histogram only allows selecting the number of bins, not their size.
    * **Solution:** The final solution was to engineer the data at the source. A **Calculated Column** was added to the Dataset using a `FLOOR()` SQL statement to pre-calculate the correct price bucket for every row. This allowed the standard Histogram chart to correctly display the custom bins, demonstrating a best-practice approach of solving tool limitations through data modeling.

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