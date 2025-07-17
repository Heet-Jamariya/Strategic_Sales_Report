# 📊 Strategic Sales Report

## 🎯 Project Objective
The primary objective of this project is to provide the auction management team with a powerful analytics tool. This dashboard replaces manual reporting, allowing stakeholders to track revenue, analyze sales trends, and identify key business drivers in real-time to make data-driven decisions for future auctions.

## 📖 Description
This project is a comprehensive analytics dashboard built in **Apache Superset** to provide deep insights into auction performance. The dashboard replaces manual reporting with a dynamic, self-service tool, allowing stakeholders to track revenue, analyze sales trends, and identify key business drivers in real-time.

The layout features Key Performance Indicator (KPI) cards at the top for a high-level summary, a grid of ten specialized charts for detailed analysis, and an interactive filter panel.

---

## 💡 Project Insights
Based on the analysis, several key insights were uncovered:
* The **Manufacturing / Production** sector is the most significant revenue driver.
* Geographically, **California** is the highest-grossing state for sales.
* A high volume of sales occurs at lower price points (0-100 range), indicating a healthy market for smaller items.
* Analysis of unsold items shows which industries have the most capital tied up in inventory, presenting an opportunity for targeted promotions.

---

## 🔑 Key Performance Indicators
This dashboard tracks the following core business metrics:
* Total Lots Sold
* Total Revenue
* Average Starting Price
* Average Sold Price
* % Above Starting Price
* Average High Estimate
* Unsold Lots
* Unsold Lots Starting Price

---

## 📈 Key Visualizations & Analyses
* **Geographic Analysis:** Visualized total sales revenue by US state to identify top-performing regions and focus marketing efforts.
* **Industry Segmentation:** Utilized a treemap to break down total revenue by industry, identifying "Manufacturing / Production" as the core market segment.
* **Time-Series Trend Analysis:** Tracked the volume of lots sold over time to monitor business growth and identify peak activity periods.
* **Price Point Analysis:** Created a histogram showing the distribution of sales across different price brackets, revealing that the majority of lots are sold in the 0-100 price range.
* **Pricing Strategy Evaluation:** Compared the trends of average starting prices vs. average sold amounts over time.
* **Asset-Level Revenue:** Identified which specific high-value items contributed most to overall revenue.
* **Inventory Analysis:** Analyzed the value and volume of unsold items, segmented by industry, to identify potential areas for inventory reduction.

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
* The `/screenshots` directory contains anonymized images of the final dashboard.
* The `README.md` file provides a detailed overview of the project's features, analyses, and technical solutions.
* An optional dashboard export file can be included to share the configuration.