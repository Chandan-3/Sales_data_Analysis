# Sales and Profit Analysis Using SQL

## Project Overview

This project analyses a company sales dataset using SQL. The main aim is to understand which products, categories, regions, and sub-categories generate high sales and how profitable they are.

The analysis focuses on identifying business insights such as highest sales by region, highest sales by category, and sub-categories that generate high sales but low profit.

## Dataset

The dataset used for this analysis is a sales dataset, stored in a MySQL table named:

```sql
super_store
```

The dataset contains information such as:

* Region
* Category
* Sub-Category
* Sales
* Profit
* Quantity
* Discount
* Order Date
* Customer details
* Product details

## Main Business Question

The main question for this analysis is:

**Which sub-categories generate the highest sales but low profit?**

This question is important because high sales do not always mean high profit. Some products may sell a lot but generate very little profit due to high discounts, high costs, or low margins.

## SQL Approach

To answer this question, the data is grouped by sub-category. Then, total sales and total profit are calculated using aggregate functions.

The main SQL functions used are:

```sql
SUM()
GROUP BY
ORDER BY
LIMIT
```

## Query 1: Total Sales and Profit by Sub-Category

```sql
SELECT 
    `sub-category`,
    SUM(sales) AS total_sales,
    SUM(profit) AS total_profit
FROM super_store
GROUP BY `sub-category`
ORDER BY total_sales DESC, total_profit ASC;
```

## Explanation

* `SUM(sales)` calculates the total sales for each sub-category.
* `SUM(profit)` calculates the total profit for each sub-category.
* `GROUP BY sub-category` groups the records based on each sub-category.
* `ORDER BY total_sales DESC` shows the highest sales first.
* `total_profit ASC` helps identify sub-categories with lower profit.

## Query 2: Profit Margin Analysis

A better way to check low profit is by calculating profit margin.

```sql
SELECT 
    `sub-category`,
    SUM(sales) AS total_sales,
    SUM(profit) AS total_profit,
    ROUND((SUM(profit) / SUM(sales)) * 100, 2) AS profit_margin_percent
FROM super_store
GROUP BY `sub-category`
ORDER BY total_sales DESC, profit_margin_percent ASC;
```

## Explanation of Profit Margin

Profit margin shows how much profit is made from sales.

For example, if a sub-category has high sales but a low profit margin, it means the company is selling many products but not making enough profit from them.

Formula used:

```sql
profit_margin = total_profit / total_sales * 100
```

## Other Useful Queries

### Which region generates the highest sales?

```sql
SELECT 
    region,
    SUM(sales) AS total_sales
FROM super_store
GROUP BY region
ORDER BY total_sales DESC
LIMIT 1;
```

### Which category generates the highest sales?

```sql
SELECT 
    category,
    SUM(sales) AS total_sales
FROM super_store
GROUP BY category
ORDER BY total_sales DESC
LIMIT 1;
```

### What is the highest single sale?

```sql
SELECT 
    MAX(sales) AS highest_single_sale
FROM super_store;
```

### Which sub-category has the highest total profit?

```sql
SELECT 
    `sub-category`,
    SUM(profit) AS total_profit
FROM super_store
GROUP BY `sub-category`
ORDER BY total_profit DESC
LIMIT 1;
```

## Key Learning

This analysis shows the difference between sales and profit.

A sub-category may have high sales, but if the profit is low, it may not be very beneficial for the business. That is why it is important to analyse both sales and profit together.

## Conclusion

The SQL analysis helps identify which sub-categories perform well in sales but poorly in profit. This can help the business review pricing, discount strategies, product costs, and sales performance.

High sales with low profit may indicate that the company needs to reduce discounts, increase prices, or investigate product costs.
