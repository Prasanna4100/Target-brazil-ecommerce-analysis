# Target-brazil-ecommerce-analysis
SQL-based analysis of Target Brazil's e-commerce dataset to uncover customer behavior, sales trends, payment preferences, logistics performance, and business growth opportunities.

## Project Overview

This project analyzes Target Brazil's e-commerce dataset to understand customer behavior, sales performance, payment preferences, logistics efficiency, and regional business trends. The objective was to uncover actionable insights that support revenue growth, operational efficiency, and improved customer experience.

**Analysis based on sales, freight and delivery time 
**
1. Find the no. of days taken to deliver each order from the order’s purchase date as 
delivery time. 
Also, calculate the difference (in days) between the estimated & actual delivery date of an 
order. 
Do this in a single query. 
 
You can calculate the delivery time and the difference between the estimated & actual 
delivery date using the given formula: 
 time_to_deliver = order_delivered_customer_date - order_purchase_timestamp 
 diff_estimated_delivery = order_delivered_customer_date - 
order_estimated_delivery_date 
 
SQL Query: 
SELECT order_id, 
    DATE_DIFF(DATE(order_delivered_customer_date), 
        DATE(order_purchase_timestamp), 
        DAY 
    ) AS time_to_deliver, 
    DATE_DIFF( 
        DATE(order_delivered_customer_date), 
        DATE(order_estimated_delivery_date), 
        DAY 
    ) AS diff_estimated_delivery 
FROM `prasanna-kumars-project.Business_Case.orders` 
WHERE order_delivered_customer_date IS NOT NULL; 
Output: 
 
Insight: 
Comparing actual and estimated delivery dates provides valuable insights into delivery 
efficiency, fulfilment accuracy, and overall customer service performance. 
Actionable Recommendations: 
 Reduce delivery delays by strengthening coordination and communication with 
logistics partners.  
 Identify and closely monitor regions with consistently longer delivery times to 
address operational bottlenecks.  
 Improve delivery forecasting and estimation processes to better align expected and 
actual fulfilment timelines. 
___________________________________________________________________________ 
2. Find out the top 5 states with the highest & lowest average freight value. 
SQL Query: 
Top 5 Highest Average Freight Value 
SELECT c.customer_state,  ROUND(AVG(oi.freight_value), 2) AS highest_avg_freight 
FROM `prasanna-kumars-project.Business_Case.order_items` as oi 
JOIN `prasanna-kumars-project.Business_Case.orders` as o 
ON oi.order_id = o.order_id 
JOIN `prasanna-kumars-project.Business_Case.customers` as c 
ON o.customer_id = c.customer_id 
GROUP BY c.customer_state 
ORDER BY highest_avg_freight DESC 
LIMIT 5 
Output: 
Top 5 Lowest Average Freight Value 
SELECT c.customer_state,  ROUND(AVG(oi.freight_value), 2) AS lowest_avg_freight 
FROM `prasanna-kumars-project.Business_Case.order_items` as oi 
JOIN `prasanna-kumars-project.Business_Case.orders` as o 
ON oi.order_id = o.order_id 
JOIN `prasanna-kumars-project.Business_Case.customers` as c 
ON o.customer_id = c.customer_id 
GROUP BY c.customer_state 
ORDER BY lowest_avg_freight ASC 
LIMIT 5 
Output: 
Insight: 
Freight costs differ significantly across states, reflecting variations in transportation distance, 
logistics efficiency, and regional infrastructure. 
Actionable Recommendations: 
 Optimise delivery routes and warehouse locations in high-cost regions.  
 Apply best logistics practices from low-cost states across the network.  
___________________________________________________________________________ 
3. Find out the top 5 states with the highest & lowest average delivery time. 
SQL Query: 
Top 5 States with Highest Average Delivery Time 
SELECT 
c.customer_state,ROUND(AVG(DATE_DIFF(DATE(o.order_delivered_customer_date),DATE(o.
order_purchase_timestamp),DAY)),2) AS hightest_avg_delivery_days 
FROM `prasanna-kumars-project.Business_Case.orders` as o 
JOIN `prasanna-kumars-project.Business_Case.customers` as c 
ON o.customer_id = c.customer_id 
WHERE o.order_delivered_customer_date IS NOT NULL 
GROUP BY c.customer_state 
ORDER BY hightest_avg_delivery_days DESC 
LIMIT 5 
Output: 
Top 5 States with Lowest Average Delivery Time 
SELECT 
customer_state,ROUND(AVG(DATE_DIFF(DATE(o.order_delivered_customer_date),DATE(o.or
der_purchase_timestamp),DAY)),2) AS lowest_avg_delivery_days 
FROM `prasanna-kumars-project.Business_Case.orders` as o 
JOIN `prasanna-kumars-project.Business_Case.customers` as c 
ON o.customer_id = c.customer_id 
WHERE o.order_delivered_customer_date IS NOT NULL 
GROUP BY c.customer_state 
ORDER BY lowest_avg_delivery_days ASC 
LIMIT 5 
Output: 
Insight: 
Average delivery time differs across states, indicating variations in logistics and fulfilment 
efficiency. 
Actionable Recommendations: 
 Investigate delays in states with longer delivery times.  
 Improve collaboration with logistics partners.  
___________________________________________________________________________ 

## Problem Statement

How can Target Brazil leverage historical e-commerce transaction data to identify growth opportunities, optimize logistics operations, improve customer satisfaction, and support data-driven business decisions?

## Tools Used

* SQL
* Google BigQuery
* Excel
* Data Analysis
* Exploratory Data Analysis (EDA)

## Key Analysis Areas

* Exploratory Data Analysis (EDA)
* Order Growth & Seasonality Analysis
* Regional Customer & Sales Distribution
* Revenue & Freight Cost Analysis
* Delivery Performance Evaluation
* Payment Behavior Analysis

## Key Insights

* Order volume increased significantly between 2016 and 2018, indicating strong business growth.
* Customer purchasing activity was highest during afternoon hours.
* Revenue and customer concentration were highest in a few major states.
* Freight costs and delivery times varied considerably across regions.
* Several states consistently delivered orders ahead of estimated delivery dates.
* Installment payments emerged as the most preferred payment method.

## Business Recommendations

* Focus marketing campaigns on high-performing regions and peak demand periods.
* Optimize logistics operations in states with higher freight costs and longer delivery times.
* Replicate successful delivery practices from top-performing states.
* Promote popular installment payment options to improve conversion rates.
* Use seasonality trends to improve forecasting and inventory planning.

## Repository Contents

* SQL Queries
* Business Case Study Report
* Analysis Documentation

## Outcome

The analysis demonstrated how SQL can be used to transform raw transactional data into actionable business insights that support strategic decision-making and operational improvements.
