# SQL-Project-2---Retail_Sales-Beginner-

# Retail Sales SQL (Beginner)

![SQL](https://img.shields.io/badge/Language-SQL-blue?logo=sqlite)
![MySQL](https://img.shields.io/badge/Database-MySQL-orange?logo=mysql)
![Beginner Friendly](https://img.shields.io/badge/Level-Beginner-green)
![Project Type](https://img.shields.io/badge/Project-Data%20Analysis-yellow)

SQL project for Retail Sales analysis – database creation, data cleaning, and business-focused queries for beginner-level practice.

---

## 📌 Project Overview

This project contains SQL scripts and queries for analyzing a **Retail Sales dataset**. It demonstrates the process of creating a database, cleaning data, and performing exploratory analysis with structured SQL queries.

---

## 🔑 Key Features

* **Database Creation**

  * Script to create the `RETAIL` database and `RETAIL_SALES` table.

* **Data Cleaning**

  * Identifying and removing `NULL` values to ensure data quality.

* **Exploratory Data Analysis (EDA)**

  * Count of total sales and unique customers
  * Listing available product categories

* **Business-Oriented SQL Queries**

  * Daily sales analysis
  * Category-level performance
  * Customer segmentation and top customers by sales
  * Gender- and category-wise transactions
  * Average sales by month & identifying best-selling periods
  * Time-of-day (shift-based) sales insights

---

## 🎯 Learning Outcomes

This project is designed for **beginner SQL learners** to practice:

* Writing `SELECT` queries with conditions, grouping, and aggregation
* Using functions like `COUNT`, `SUM`, `AVG`, `DATE_FORMAT`, and `EXTRACT`
* Applying window functions (`RANK()`) for ranking best-performing months
* Solving **real-world business problems** with SQL

---

## 📂 File Included

* `Retail_Sales - SQL (Beginner).sql` → Complete SQL script with:

  * Database setup
  * Data cleaning
  * 10+ business-focused analysis queries

---

-- CREATING THE TABLE 
```sql
CREATE TABLE RETAIL_SALES(
transactions_id	INT PRIMARY KEY,
sale_date DATE,
sale_time TIME,
customer_id	INT,
gender VARCHAR(15),
age	INT,
category VARCHAR(15),
quantiy	INT,
price_per_unit	FLOAT,
cogs FLOAT,
total_sale FLOAT
);
```

---

# Data Analysis & Bussiness key problems and answers

### **My Analysis & Findings :**

1. Write a SQL query to retrieve all columns for sales made on '2022-11-05?
2. Write a SQL query to retrieve all transactions where the category is 'Clothing' and the quantity sold is more than 4 in the month of Nov-2022?
3. Write a SQL query to calculate the total sales (total_sale) for each category?
4. Write a SQL query to find the average age of customers who purchased items from the 'Beauty' category?
5. Write a SQL query to find all transactions where the total_sale is greater than 1000?
6. Write a SQL query to find the total number of transactions (transaction_id) made by each gender in each category?
7. Write a SQL query to calculate the average sale for each month. Find out best selling month in each year?
8. Write a SQL query to find the top 5 customers based on the highest total sales?
9. Write a SQL query to find the number of unique customers who purchased items from each category?
10. Write a SQL query to create each shift and number of orders (Example Morning <=12, Afternoon Between 12 & 17, Evening >17)?

---

## Queries :

Q.1 Write a SQL query to retrieve all columns for sales made on '2022-11-05'?
```sql
SELECT * FROM 
RETAIL_SALES
WHERE sale_date = '2022-11-05';
```


Q.2 Write a SQL query to retrieve all transactions where the category is 'Clothing' and the quantity sold is more than 4 in the month of Nov-2022?
```sql
SELECT * FROM RETAIL_SALES
WHERE category = 'Clothing' 
		AND 
        DATE_FORMAT(sale_date, '%Y-%m') = '2022-11'
		AND 
        quantiy >= 4;
```

        
Q.3 Write a SQL query to calculate the total sales (total_sale) for each category?
```sql
SELECT RETAIL_SALES.CATEGORY, 
		SUM(TOTAL_SALE) AS TOTAL_SALES,
        COUNT(*) AS TOTAL_ORDERS
FROM RETAIL_SALES
GROUP BY RETAIL_SALES.CATEGORY;
```


Q.4 Write a SQL query to find the average age of customers who purchased items from the 'Beauty' category?
```sql
SELECT ROUND(AVG(age), 2) AS AVG_AGE
FROM RETAIL_SALES
WHERE CATEGORY = 'BEAUTY';
```


Q.5 Write a SQL query to find all transactions where the total_sale is greater than 1000?
```sql
SELECT *
FROM RETAIL_SALES
WHERE total_sale >= 1000;
```


Q.6 Write a SQL query to find the total number of transactions (transaction_id) made by each gender in each category?
```sql
SELECT GENDER,CATEGORY, COUNT(transactions_id)
FROM RETAIL_SALES
GROUP BY GENDER, CATEGORY;
```


Q.7 Write a SQL query to calculate the average sale for each month. Find out best selling month in each year?
```sql
SELECT 
	EXTRACT(YEAR FROM sale_date) AS YEAR,
    EXTRACT(MONTH FROM sale_date) AS MONTH,
    ROUND(AVG(TOTAL_SALE),2) AS AVG_SALES,
    RANK() OVER(PARTITION BY EXTRACT(YEAR FROM sale_date)  ORDER BY AVG(TOTAL_SALE) ) AS BEST_SELLING_YEAR
FROM RETAIL_SALES
GROUP BY 1, 2;
-- ORDER BY 1, 3 DESC;
```


Q.8 Write a SQL query to find the top 5 customers based on the highest total sales?
```sql
SELECT customer_id,
		SUM(total_sale) AS TOTAL_SALES
 FROM RETAIL_SALES
 GROUP BY customer_id
 ORDER BY TOTAL_SALES DESC
 LIMIT 5;
```


Q.9 Write a SQL query to find the number of unique customers who purchased items from each category?
```sql
SELECT category,
		COUNT(DISTINCT customer_id) AS CUSTOMER_ID,
        SUM(TOTAL_SALE) AS TOTAL_SALES
FROM RETAIL_SALES
GROUP BY category;
```


Q.10 Write a SQL query to create each shift and number of orders (Example Morning <=12, Afternoon Between 12 & 17, Evening >17)?
```sql
SELECT  *, 
	CASE
		WHEN EXTRACT(HOUR FROM sale_time) < 12 THEN "MORNING"
        WHEN EXTRACT(HOUR FROM sale_time) BETWEEN 12 AND 17 THEN "AFTERNOON"
        ELSE "EVENING"
	END AS SHIFT
FROM RETAIL_SALES;
```

--- 

## 🚀 Usage

1. Open MySQL or your preferred SQL environment.
2. Run the script `Retail_Sales - SQL (Beginner).sql`.
3. Explore and modify queries to practice or adapt them for other datasets.

---

## 📖 License

This project is for learning and practice purposes. Feel free to fork and modify it for your own SQL journey.

