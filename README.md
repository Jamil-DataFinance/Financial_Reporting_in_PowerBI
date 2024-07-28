
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

SELECT

--FactGLTran
gl.FactGLTranID,
gl.GLTranAmount,
gl.JournalID,
gl.GLTranDescription,
gl.GLTranDate,

--GL Accounts
acc.AlternateKey 'GLAcctNum',
acc.GLAcctName,
acc.Statement,
acc.Category,
acc.Subcategory,

--Stores
sto.AlternateKey 'StoreNum',
sto.StoreName,
sto.ManagerID,
sto.PreviousManagerID,
sto.ContactTel,
sto.AddressLine1,
sto.AddressLine2,
sto.ZipCode,

--Region
reg.AlternateKey 'RegionNum',
reg.RegionName,
reg.SalesRegionName,

--Last Refresh Date
CONVERT(datetime2, GETDATE() at time zone 'UTC' at time zone 'Central Standard Time') AS 'LastRefreshDate'

FROM FactGLTran AS gl
    INNER JOIN dimGLAcct AS acc ON gl.GLAcctID = acc.GLAcctID
    INNER JOIN dimStore AS sto ON gl.StoreID = sto.StoreID
    INNER JOIN dimRegion AS reg ON sto.RegionID = reg.RegionID


**Above query has been uploaded to power BI using connection with Microsoft server**

**2. Data CLeaning and Tranformation**

In Power Query Editor, I did not need to clean the data since it was already processed in SQL. My task was to split the consolidated table into separate Fact and Dimension tables. I handled duplication issues that arose from SQL inner joins by using the "Remove Duplicates" option for all tables except the Fact table.

**3. Data Model**


The data model follows a snowflake schema, which is illustrated in the attached picture. This schema involves a central Fact table surrounded by normalized Dimension tables, enhancing data organization and reducing redundancy. 


![Star Schema](https://github.com/user-attachments/assets/0e4fc248-967a-4a4d-95fe-01adb6ed0551)


**4. Reporting**

In the reporting stage, I adopted a step-wise approach, keeping measures organized by their respective reports. This method ensures clarity and maintains a clear structure, with each measure directly related to the specific report it supports.

**Income Statement**

As out dataset is connected to a single database, it will have values of income statement and balance sheet. we need to explicitly define income statement values using below measure. 

I/S Amount = 					
					
CALCULATE([SUM Amount],Dim_Headers[Statement] = "Income Statement")


Subtotals like Gross Profits, operating profits, net profits are calculated using below measure. 

I/S Subtotal = 				
				
CALCULATE(				
    [I/S Amount],				
    FILTER(				
        All(				
            Dim_Headers),Dim_Headers[Sort]<MAX(Dim_Headers[Sort])))				



Ratios can be calculated using below measures

% of Revenue = 							
							
VAR Revenue = CALCULATE([I/S Amount],FILTER(ALL(Dim_Headers),Dim_Headers[Category]="Revenue"))							
							
Return 							
DIVIDE([I/S Subtotal],Revenue,0)							



**Challenege**

Now we have three separate measures , I/s Amount, I/S subtotal and Ratios. we need to combine these measures to make it relevant for us. 

We will write a master measure which will be called **Income statement measure**


Income Statement = 						
SWITCH(TRUE(),						
SELECTEDVALUE( Dim_Headers[MeasureName])="Subtotal",[I/S Subtotal],						
SELECTEDVALUE( Dim_Headers[MeasureName])="Per_Of_Revenue",[% of Revenue],						
    [I/S Amount]						
)						



**Another challenge**
Now our dataset show revenues as negative numbers and expenses as positive. we need to show all numbers in positive. 

we will use absulte function to show all values positive. 

I/S Amount = 						
						
CALCULATE(ABS([SUM Amount]),Dim_Headers[Statement] = "Income Statement")		

**Final Step- Creating charts**

To show **water fall charts** for revenues and expenses , we need to flip the sign for all income statement amounts . this can be achieved using below measure. 

				
	SumAmount- WaterFall Chart = [SUM Amount] * -1			
				
please note that above measure has no other use except using in water fall chart


**Gross profit margin** can be calculated using below measure:

Gross Profit Ratio = 						
						
VAR Gross_profit = CALCULATE([I/S Subtotal],Dim_Headers[Category]="Gross Profit")						
VAR Revenue = CALCULATE([I/S Amount],Dim_Headers[Category]="Revenue")						
						
Return 						
DIVIDE(Gross_profit,Revenue,0)				


**Report Refresh Date**
Query has already been calculated in SQL for report refresh date , now we just need to remove all duplicates from the column and paste date in the card visuals. 



#Below is the complete income statement 


![Income Statement](https://github.com/user-attachments/assets/4b1b69e8-7fc4-4fb0-809e-e605decd4e8e)







































