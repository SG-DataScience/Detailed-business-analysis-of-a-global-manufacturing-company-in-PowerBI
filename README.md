
#	Detailed Business Analysis of a Globale Manufacturing Company in PowerBI:

## Project Description:
This project deals with the total end to end business intelligence solution for a global manufacturing company which includes --

- Tracking KPI of sales, profit, returns and revenue.
- Compare product level trends.
- Identify high value customers.
- Analyze regional performance.
- Forecast.

We have been provided with some raw csv files which contain all the data of the company, related to the transactions, 
returns, products, customers and territories.

## Project Pipeline:

![sandipa](https://user-images.githubusercontent.com/80168511/153021060-57b801fe-ae7d-4535-9b87-6949a87f6068.png)

## Project Walkthrough:
### 1. Loading the csv files:
we have connected the source folder( where we have kept all the data of the company) to Power BI and loaded the raw csv files.Then we have made several changes to all the tables, according to our needs.
### 2. Reshaping the data:
In the query editor we have made some changes to the imported data like--
- Renamed the tables
- Changed the data type of the columns, wherever required
- Removed the unnecessary columns
- Added some new columns in some of the tables
- Formatted some of the fields
### 3. Building the data model:
In this part we have connected all the tables via relationship, based on their common fields.
#### Relationship between the Sales table and the lookup tables are as follows --
    1. Customer lookup (CustomerKey) --> Sales (CustomerKey)
    2. Calendar lookup (Date) --> Sales(OrderDate)
    3. Territories lookup (SalesTerritoryKey) --> Sales(TerritoryKey)
    4. Product lookup (ProductKey) --> Sales(ProductKey)

#### Relationship between the Returns table and the lookup tables are as follows--
    1. Calendar lookup (Date) --> Returns(ReturnDate)
    2. Territories lookup (SalesTerritoryKey) --> Returns(TerritoryKey)
    3. Product lookup (ProductKey) --> Returns(ProductKey)

We have created a snowflake schema by creating relationship from Product lookup table to Product Subcategory table and Product Subcategory to Product Category table, as the Sales and Returns table can not be connected directly to the Product Category and Product Subcategory tables.Now this snowflake schema will aid the proper filter context to flow down the chain. 

### 4. Creating Some Calculated Fields: 
After building the data model we have created some calculated columns and measures using DAX and used some of them for the analysis and visualization of the data. The most important among them, which has been directly used to design the visualization report, are as follows--
- Calculated Measures:
Total Order, Total Cost, Total Revenue, Total Profit, Return Rate, Total Returns, Prev Month Revenue, Prev Month Orders, Prev Month Returns, Order Target, Revenue Target, Adjusted Profit, Adjusted Price, Avg Retail Price etc.
- Calculated Columns:
Current Age, Quantity Type, Price Point etc.

### 5. Designing the Visualization Report:
The final visual report mainly consist of 3 pages--
#### 1. Overall Summary (First Page) :
- In this page we have created a Matrix which shows the Total Orders and Return Rate(in %) based on the Product Category. To analyze it in more detail, we can easily drill up or down to check the info of the Subcategory and the Product Name. Condional formatting has been applied to make it more interactive.
- A tree map has been added to visualize the Total Orders based on Category.As we have added Total Profit in the tooltip section, so this info is also visible in this tree map.
- Then we have added a stacked bar chart to visualize Total Orders by Subcategory and here also Total Revenue has been added to the tooltip section.
- Now we have used 3 KPI to showcase the Monthly Revenue, Monthly Orders and Monthly Returns. Also a target goal (of their respective previous month's value) has been set up for each of them.
- Then we have added 2 cards, one to show the top product by orders and another to show the top product by profit.
- A map has been added (which works on updated version of PowerBI).
- In this page, we have used 2 slicers-- One is Date slicer another one is continent slicer.
- In the bottom of this page, we have added a bookmark icon which connects to the product detail page.
The First Page looks like --
![p1](https://user-images.githubusercontent.com/80168511/153022631-5f10a1d0-ab4f-409f-a2fc-eae099c515b4.PNG)

#### 2. Product Detail (Second Page) :
This page deals with the information about the products.

First of all, in this page we have added "Product Name" as the Drill-Through field.Due to additon of this filter now we can access the details of our required poroduct from any of the pages in this whole report. Just we need to right click on that product name and select the Drill throuh option to reach to the Product Detail page directly, which will show all the info of our selected product.
- Firstly a card has ben added which shows the product name (i.e. the required product, about which we wanted to know in detail).
- Then we have inserted 3 gauge charts which shows current month orders vs the order target (10% more than the previous month's order), current month revenue vs revenue target (10% more than the previous month's revenue), current month returns vs previous month's returns.
- Now a line chart has been added which visualizes the weekly profit (also the total order and total revenue of each week). A trend line as well as the forecast of 10 weeks (with a confidence interval of 95%) has also been added to the chart.
- Then an area chart has been added which depicts the weekly returns.
- To make this page more dynamic, from the modeling tab we have generated a slicer (price adjustment %) using what-if parameter. The slicer contains a series of values where the minimum value is -1 and the maximum value is +1, with an increment of 10%.
- Using this price adjustment %, two measures has been created - adjusted price and adjusted profit. Now we have added a line chart which visualizes the difference between the adjusted profit's values (according to the selected value in slicer) and the actual total profit.
- At last we have added a multi-row card which shows the Avg Retail Price and the Adjusted Price (referring to the slicer).
The Second Page looks like --
![p2](https://user-images.githubusercontent.com/80168511/153022661-d645498b-9b68-4672-a0b4-5a877ed4559e.PNG)

### 3. Customer Detail (Third Page) :
As its name suggests, this page contains the customer details.
- Firstly, a Matrix has been added which shows the top 100 (based on total revenue) customer's info -- full name, total orders and total revenue.
- Then we have inserted 3 donut charts. First shows the total orders based on gender, second shows the total orders by income level and third shows the total orders by occupation.
- A line and clustered column chart has been inserted to show the total orders (as columns) and total revenue (as a line), with start of month on the shared x-axis.
- Now a tree map was added to show total orders (values) grouped by current age.
- Then we have inserted 3 cards which shows the full name, total orders and total revenue of the top customer based on the total revenue.
- At the bottom of the page we have inserted a arrow button which connects to the Overall Summary page.
The Customer Detail page looks like --
![p3](https://user-images.githubusercontent.com/80168511/153022688-42ddeb27-fbef-4f4b-b145-bd23be136f56.PNG)
#### In this entire dashboard we have set up a report level filter on year, so that all the inforamtion should be of year 2016 and 2017.
