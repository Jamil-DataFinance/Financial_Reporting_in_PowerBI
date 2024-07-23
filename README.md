# Financial_Reporting_in_PowerBI

# Overview
This project showcases a comprehensive financial reporting dashboard built in Power BI, using data sourced from an SQL database. The dashboard provides real-time insights into financial performance, featuring detailed income statements, balance sheets, and cash flow statements.

# Features

**Real-Time Data Integration:** Connects to an SQL database for up-to-date financial data.

**Interactive Visualizations:** Dynamic charts and graphs for detailed financial analysis.

**Comprehensive Financial Statements:** Includes income statements, balance sheets, and cash flow statements.

**User-Friendly Interface:** Easy to navigate with dynamic filtering and drill-down capabilities

# Technologies Used

**Power BI:**  For data visualization and dashboard creation.
**SQL:** For data storage and real-time data integration.

# Process 
I can split this process into 4 Major Steps and Few Challenges 

**1. Data Connection**

Our database had a well-structured schema with fact and dimension tables. I created a consolidated view by writing a SQL query to combine these tables into a single table. This approach ensures real-time data updates and prevents data loss during refreshes. The view was then connected to Power BI, and I incorporated the GETDATE() function to track query refresh dates.












