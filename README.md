
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

**Below is the SQL query used to gather the data**

![image](https://github.com/user-attachments/assets/b6fd57d5-e0a7-4236-be41-8d6753510d8a)

**Above query has been uploaded to power BI using connection with Microsoft server**

**2. Data CLeaning and Tranformation**

In Power Query Editor, I did not need to clean the data since it was already processed in SQL. My task was to split the consolidated table into separate Fact and Dimension tables. I handled duplication issues that arose from SQL inner joins by using the "Remove Duplicates" option for all tables except the Fact table.

**3. Data Model**


The data model follows a snowflake schema, which is illustrated in the attached picture. This schema involves a central Fact table surrounded by normalized Dimension tables, enhancing data organization and reducing redundancy. 


![Star Schema](https://github.com/user-attachments/assets/0e4fc248-967a-4a4d-95fe-01adb6ed0551)


**4. Reporting**

In the reporting stage, I adopted a step-wise approach, keeping measures organized by their respective reports. This method ensures clarity and maintains a clear structure, with each measure directly related to the specific report it supports.

**Income Statement**


Preparation of the income statement can be divided into three main components: calculation of amounts, subtotals, and ratios. 


The calculation of income statement amounts is straightforward and can be achieved using the following simple measure. It is essential to explicitly define the income statement amount using this measure


![image](https://github.com/user-attachments/assets/a238364e-924f-4c66-bbb9-0f4d066435f8)



Subtotals like gross profits, operating profits, and net profits are determined using the measure below. These subtotals are treated as running totals, achievable with the specified calculation


![image](https://github.com/user-attachments/assets/97f84325-eda7-4e7a-ba79-dc5dc8306ebe)



Finally, ratios are calculated as a percentage of revenue using the following measure


![image](https://github.com/user-attachments/assets/293e56ce-cae6-4590-8a25-28aabe7a0b32)
					

**Challenege No. 1**


Now, we have three distinct measures: I/S Amount, I/S Subtotal, and Ratios. To make these measures relevant and useful, we need to combine them. We will create a master measure called the "Income Statement Measure


![image](https://github.com/user-attachments/assets/2763cb65-98a5-41ab-b5f7-8be3603c26d4)
				


**Challenege No.2**
Currently, our dataset displays revenues as negative numbers and expenses as positive. To present all values as positive, we will use the absolute function

![image](https://github.com/user-attachments/assets/eb7a1f0a-3373-4258-87ff-4825bd7e5b90)
		


**Chellenge No. 3**

To display waterfall charts for revenues and expenses, we need to flip the sign of all income statement amounts. This can be achieved using the following measure
				
	SumAmount- WaterFall Chart = [SUM Amount] * -1			
				
please note that above measure has no other use except using in water fall chart


**Gross profit margin** can be calculated using below measure:


![image](https://github.com/user-attachments/assets/d390589d-69ac-410e-af6f-db78cd9e7e07)
		

**Report Refresh Date**
The query for the report refresh date has already been calculated in SQL. Now, we simply need to remove all duplicates from the column and display the date in the card visuals

# Below is the complete income statement 


![Income Statement](https://github.com/user-attachments/assets/4b1b69e8-7fc4-4fb0-809e-e605decd4e8e)


# Balance Sheet

The balance sheet presents similar challenges as the income statement. The final measure for the balance sheet is shown below


![image](https://github.com/user-attachments/assets/4229ea23-5a38-467f-83f0-2a541f2149c0)


# Final Balance sheet would be:

![Balance Sheet](https://github.com/user-attachments/assets/c0c614b0-ff62-4c3c-8fe6-1f9695570f03)



# Cash Flowe statement 

Since cash flow calculations differ from those of the income statement and balance sheet, we need to explicitly write a measure for almost each line item. 

We will use the SELECTEDVALUE measure with the SWITCH TRUE function to obtain all relevant values


![image](https://github.com/user-attachments/assets/07749b16-a1ab-4691-ac54-2e1d4b5553c8)


# Final Cash flow statement would be:

![Cash Flow Statement](https://github.com/user-attachments/assets/ae0b51e1-507f-4bfe-822a-74dba400fae7)




# Convert to Monthly Model 

Currently, our reports are displayed on a yearly basis. We can easily switch the model to a monthly basis by changing the column values from years to months, resulting in the following outcomes


![Detailed Income Statement](https://github.com/user-attachments/assets/710e6b78-cd62-4df3-bba6-6dfd7cac920f)


# Ensure Report Accuracy 

We can apply the following checks to ensure the accuracy of all three financial statements:


**Income statements**

![image](https://github.com/user-attachments/assets/4ba1b008-d9fe-4c10-bc54-584f7bedb5af)


**Balance sheet**


I explicitly defined a tolerance level because our balance sheet was not balancing by 0.34, resulting in an imbalance

![image](https://github.com/user-attachments/assets/cdb698ea-bd5c-4829-bd61-09b6a1766336)


**Cash Flow Statement**

![image](https://github.com/user-attachments/assets/7e584642-9ead-4c5a-870a-f11303a76b73)


# Whole idea behind installing checks

Checks were implemented for all three statements to ensure the measures match our staging fact table. If they do not match, it indicates an issue in our report

![image](https://github.com/user-attachments/assets/a7c1c91c-a2ab-4634-b42d-6637738f107e)


# Contact

For any questions or further information, please contact:

https://www.linkedin.com/in/jamil-ur-rehman-acca/

Jamil.akhunzada@gmail.com

+971566353172




























