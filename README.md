# Pizza_Sales_analysis_project

## Table of content
- [Project overview](#project-overview)
- [Data Sources](#data-sources)
- [Tools Used](#tools-used)
- [Data cleaning](#data-cleaning-preparation)
- [Exploratory Data Analysis](#exploratory-data-analysis)
- [Data Analysis](#data-analysis)
- [Results/Findings](#results/findings)
- [Recommendations](#recommendations)

# Project overview
This data analysis project aims to provide detailed insights into the sales performance of an e-commerce company that specialises in selling pizza. By analysing the various aspects of sales, we seek to identify trends, make data-driven decisions, and gain a deeper understanding of the company’s performance.

## Data Sources

Sales Data - the primary source used for this analysis is the “pizza_sale(1).csv” file, containing detailed information about the sales activity of the company.

## Tools Used
- Excel - Data Cleaning
- Sql Server - For Data Analysis
- PowerBi - For creating Report

## Data cleaning/preparation
In the initial preparation phrase, we performed the following tasks:
- Data loading and inspection
- Handling missing values
- Data cleaning and formatting

## Exploratory Data Analysis (EDA)
EDA involved exploring the sales data to answer the following questions:
- What is the Total Revenue
- What is the Average Order value?
- What is the total number of pizzas sold?
- What is the total number of orders placed?
- What is the average number of pizzas sold per order?
- What is the percentage of sales by pizza category?
- What is the hourly, daily and monthly trend for total orders?
- What is the percentage of sales by pizza size?
- What is the total number of pizzas sold by pizza category?
- What are the top five best selling pizzas by revenue, quantity and total orders?

## Data Analysis

``` Sql queries
-- Percentage of sales by pizzas category
select pizza_category,
       sum(total_price) as Total_sales,
       cast(sum(total_price)*100/(select sum(total_price) from [pizza_sales (1)] where datepart(quarter,order_date)=1) as decimal(10,2)) as pct_of_total_sales 
from [pizza_sales (1)] where datepart(quarter,order_date) = 1
group by pizza_category
order by 3 desc

-- Hourly Trend for total orders
select datepart(hour,order_time) as hr,
          count(distinct order_id) as Total_orders
from [pizza_sales (1)]
group by datepart(hour,order_time)
order by 2 desc

-- Average pizzas per order
select cast(cast(sum(quantity) as decimal (10,2))/cast(count(distinct order_id) as decimal(10,2))
as decimal(10,2))as Avg_pizzas_per_order
from [pizza_sales (1)]
```



## Results/Findings
The analysis results are summarised as follows:
- Orders are highest towards the weekend: Thursday, Friday and Saturday
- Maximum orders are seen in the months of January and July
- The Classic pizza is the best performing pizza category in terms of sales and orders
- The large sized pizza has the maximum sales.
- Maximum orders were placed around the hours of 12pm and 1pm


## Recommendations
Based on the analysis we recommend the following actions:
- Invest in marketing and promotions during peak hours, days and months to maximise revenue
- Focus on expanding and promoting the Classic category, with emphasis on the large sized pizza
