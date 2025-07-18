# Case Study: Strategic Sales Report Dashboard

> **Note:** This is the text-based version of the case study for GitHub. For a more visual experience with embedded screenshots and professional formatting, please view the full case study document.
> ### ➡️ [**View the Full Visual Case Study (Google Doc)**](https://docs.google.com/document/d/10xZssYWOhIzqghM30zAqdMFC5BcLZPhLcYrfeo4dLxM/edit?usp=sharing)

---

### 1. Project Inception & My Role
As a new member of the data team, my journey on this project began when I was entrusted with the database credentials by my team lead. My initial directive was to connect to the data, perform a thorough exploration of the schema, and build a comprehensive sales dashboard to identify key trends and performance metrics. This foundational analysis and development was crucial for providing the business with a new, interactive way to view their sales data.

---

### 2. The "Design" Phase: The Blueprint
The final design was guided by a professional **Figma prototype** provided by the project lead. This prototype served as the blueprint, outlining the required look and feel for the dashboard. It specified the eight core KPIs (like Total Revenue and % Above Starting Price) and provided mockups for advanced charts, including "Revenue Breakdown" and "Lots Sold Over Time".

---

### 3. The "Process" Steps: From Concept to Reality
The development workflow followed a structured, iterative process:

1.  **Initial Understanding & Prototyping:** After the database orientation, 1-2 demo dashboards were created to validate data connections and establish a baseline understanding of the data's potential and limitations.
2.  **Core KPI Development:** With the final Figma design as a guide, development focused on building the high-level Key Performance Indicators (KPIs) using Superset's "Big Number" chart type.
3.  **Advanced Chart Implementation:** Development then moved to more complex visualizations. This required iterative debugging and creating calculated columns at the dataset level to handle tool limitations, particularly for the Histogram, Time-series, and Treemap charts.
4.  **Specialized Analysis:** Charts requiring advanced logic, such as the USA-only map and dual-axis trend charts, were developed to meet specific analytical requirements.
5.  **Dashboard Assembly & Filtering:** All completed charts were assembled into the final dashboard. Interactive filters were then added and configured for **cascading behavior**, allowing users to dynamically slice data across the entire dashboard.

---

### 4. The "Challenges" Story: Overcoming Hurdles

* **Challenge 1: Ensuring Accurate and Intuitive KPI Formatting**
    * **Problem:** A critical KPI, "% Above Starting Price", was displayed as a raw number (e.g., "79.87") instead of a percentage.
    * **Solution:** This involved a two-step refinement. First, the SQL query was modified to calculate the pure decimal ratio (0.7987). Second, Superset's built-in **D3 Number Formatting (`.2%`)** was applied to visually convert the ratio into a user-friendly percentage.

* **Challenge 2: Complex Trend Analysis (The Dual-Axis Chart)**
    * **Problem:** A requirement was to compare "Starting Price" and "Sold Price" trends on the same chart, which a simple line chart couldn't handle effectively.
    * **Solution:** This was solved by using Superset's **"Mixed Time-Series Chart."** This allowed for plotting two distinct metrics against a shared time axis, creating an intuitive dual-line comparison.

* **Challenge 3: Aggregating Data for Time-Series Analysis**
    * **Problem:** The raw sales data was transactional and needed to be aggregated into monthly buckets for trend analysis.
    * **Solution:** Instead of writing a complex aggregation query, I used the chart's built-in **Time Grain** setting. By specifying "Month" as the grain and `COUNT(DISTINCT catalog_id)` as the metric, Superset automatically handled the `GROUP BY` aggregation.

* **Challenge 4: Multi-Layered Geospatial Visualization**
    * **Problem:** The map component required the strict ISO 3166-2 format (e.g., "US-CA"), which was not available in the raw data.
    * **Solution:** I created a **Calculated Column** directly within the Superset dataset. Using the SQL expression `CONCAT('US-', state_state_short_code)`, a new, properly formatted column was generated on the fly to solve the issue.

* **Challenge 5: Advanced Custom Binning for Price Distribution**
    * **Problem:** The business needed to see item distribution in fixed-width price intervals (e.g., buckets of $18,000), but Superset's standard histogram only allows selecting the number of bins, not their size.
    * **Solution:** The final solution was to engineer the data at the source. A **Calculated Column** was added to the Dataset using a `CASE & END` SQL statement to pre-calculate the correct price bucket for every row. This allowed the standard Histogram chart to correctly display the custom bins, demonstrating a best-practice approach of solving tool limitations through data modeling.

---

### 5. The "Impact" Statement: Project Outcomes
The delivery of the "Sales Overview Report" provided the business with a valuable new tool for analyzing their sales performance. The dashboard successfully centralized key sales metrics into a single source of truth and delivered a significant qualitative impact.

#### Key Outcomes:
* **Enabled Self-Service Analytics:** The dashboard empowered managers to explore data on their own using interactive filters, allowing them to answer their own questions without needing technical assistance.
* **Delivered New Strategic Insights:** The visualizations surfaced previously hidden insights, such as identifying top revenue-generating sectors and providing clear data for inventory and pricing strategy.
* **Provided Real-Time Data Access:** By connecting directly to the database, the dashboard provided an up-to-date view of performance, ensuring decisions were based on the most current data available.

---

### 6. Final Summary & Key Learnings
This project was a significant learning opportunity that allowed me to manage a data visualization project from start to finish. The experience was about more than just building charts; it was a journey in translating business needs into a functional, data-driven tool.

My key takeaways from this experience include:
* **The Importance of Data Modeling:** I learned that the most effective way to overcome a BI tool's limitations is often to engineer the data correctly at the source, as demonstrated by the custom binning and geospatial challenges.
* **Iterative Development:** Regular check-ins with my team lead and stakeholders were crucial for validating data and ensuring the final product aligned with their needs.
* **From Data to Insights:** The project reinforced my understanding of how to move beyond simple reporting to create visualizations that tell a story and answer critical business questions.

Based on the dashboard's findings, I presented the following key insights to my team lead for strategic consideration:
1.  **High-Value Segments:** The Manufacturing sector represents a significant opportunity, and targeted marketing in key states like California could yield high returns.
2.  **Inventory Optimization:** The high volume of lower-priced items suggests that bundled deals or targeted promotions could be an effective strategy to increase sell-through rates.

---

### Final Note
This case study documents the end-to-end process of turning data into actionable intelligence.
