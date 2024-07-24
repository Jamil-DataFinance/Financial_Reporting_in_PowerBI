# Financial_Reporting_in_PowerBI

# Overview
This project showcases a comprehensive financial reporting dashboard built in Power BI, using data sourced from an SQL database. The dashboard provides real-time insights into financial performance, featuring detailed income statements, balance sheets, and cash flow statements.

# Check out the project below. 

https://app.powerbi.com/links/nidqvkjOOu?ctid=00333eed-6c17-42d5-9b84-c61a712c1071&pbi_source=linkShare&bookmarkGuid=8211a2b8-617a-4546-82da-e7122020a96b

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


**2. Data CLeaning and Tranformation**

In Power Query Editor, I did not need to clean the data since it was already processed in SQL. My task was to split the consolidated table into separate Fact and Dimension tables. I handled duplication issues that arose from SQL inner joins by using the "Remove Duplicates" option for all tables except the Fact table.

**3. Data Model**


The data model follows a snowflake schema, which is illustrated in the attached picture. This schema involves a central Fact table surrounded by normalized Dimension tables, enhancing data organization and reducing redundancy. 

**4. Reporting**

In the reporting stage, I adopted a step-wise approach, keeping measures organized by their respective reports. This method ensures clarity and maintains a clear structure, with each measure directly related to the specific report it supports.



