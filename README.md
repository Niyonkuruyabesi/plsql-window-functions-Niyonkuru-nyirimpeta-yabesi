# plsql-window-functions-Niyonkuru-nyirimpeta-yabesi

# PL/SQL Window Functions – Agribusiness Project

## 📌 Project Overview
This project demonstrates the use of **PL/SQL window functions** to analyze agricultural sales data.  
The goal is to apply ranking, aggregation, navigation, and distribution functions to gain business insights such as top customers, sales trends, and customer segmentation.  

---

## 🏢 Business Problem
**Context**: Agribusiness company operating in Rwanda.  
**Challenge**: The company does not know the **top-selling agricultural products** in their regions.  
**Expected Outcome**: By applying SQL window functions, the company will identify top-performing products, track revenue trends, and segment customers for better decision-making.  

---

## 🎯 Success Criteria
1. Find **Top N customers by revenue** → `ROW_NUMBER()`, `RANK()`, `DENSE_RANK()`, `PERCENT_RANK()`.  
2. Calculate **running totals and averages** → `SUM()`, `AVG()`.  
3. Track **minimum and maximum sales trends** → `MIN()`, `MAX()`.  
4. Compare **current vs previous transactions** → `LAG()`, `LEAD()`.  
5. Segment customers into **quartiles and distributions** → `NTILE(4)`, `CUME_DIST()`.  

---

## 🗄️ Database Schema
```sql
CREATE DATABASE agriculture;

CREATE TABLE customers (
    customer_id INT PRIMARY KEY,
    cust_name VARCHAR(50),
    region VARCHAR(30)
);

CREATE TABLE products (
    product_id INT PRIMARY KEY,
    prod_name VARCHAR(50),
    category VARCHAR(40)
);

CREATE TABLE transactions (
    transaction_id INT PRIMARY KEY,
    customer_id INT,
    FOREIGN KEY (customer_id) REFERENCES customers(customer_id),
    product_id INT,
    FOREIGN KEY (product_id) REFERENCES products(product_id),
    sale_date DATE,
    amount DECIMAL(10, 2)
);




-- ROW_NUMBER()
SELECT customer_id, SUM(amount) AS total_revenue,
       ROW_NUMBER() OVER (ORDER BY SUM(amount) DESC) AS row_num
FROM transactions
GROUP BY customer_id;

-- RANK()
SELECT customer_id, SUM(amount) AS total_revenue,
       RANK() OVER (ORDER BY SUM(amount) DESC) AS revenue_rank
FROM transactions
GROUP BY customer_id;

-- DENSE_RANK()
SELECT customer_id, SUM(amount) AS total_revenue,
       DENSE_RANK() OVER (ORDER BY SUM(amount) DESC) AS dense_rank
FROM transactions
GROUP BY customer_id;

-- PERCENT_RANK()
SELECT customer_id, SUM(amount) AS total_revenue,
       PERCENT_RANK() OVER (ORDER BY SUM(amount) DESC) AS percent_rank
FROM transactions
GROUP BY customer_id;

