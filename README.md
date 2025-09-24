# plsql-window-functions-Niyonkuru-nyirimpeta-yabesi

# PL/SQL Window Functions – Agribusiness Project

##  Project Overview
This project demonstrates the use of **PL/SQL window functions** to analyze sales data in an **agriculture/agribusiness company**.  
The objective is to apply **ranking, aggregation, navigation, and distribution functions** to discover top customers, sales trends, and customer segmentation insights.  

---

##  Business Problem
**Context**: Agribusiness operating across regions in Rwanda.  
**Challenge**: The company does not know the **top-selling agricultural products** in each region.  
**Expected Outcome**: By applying SQL window functions, the company can identify top products, track monthly revenue growth, and segment customers for marketing strategies.  

---

##  Success Criteria
1. Identify **Top customers by revenue** → `ROW_NUMBER()`, `RANK()`, `DENSE_RANK()`, `PERCENT_RANK()`.  
2. Compute **running totals and averages** → `SUM()`, `AVG()`.  
3. Track **minimum and maximum sales trends** → `MIN()`, `MAX()`.  
4. Compare **previous vs next transactions** → `LAG()`, `LEAD()`.  
5. Segment customers into **quartiles and distributions** → `NTILE(4)`, `CUME_DIST()`.  

---

##  Database Schema
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
    amount DECIMAL(10,2)
);
```

DATA INSERTION

1. CUSTOMERS TABLE
```SQL
INSERT INTO customers VALUES (1, 'Yabesi', 'Musanze');
INSERT INTO customers VALUES (2, 'Niyonkuru', 'Rubavu');
INSERT INTO customers VALUES (3, 'Nyirimpeta', 'Gasabo');
INSERT INTO customers VALUES (4, 'Rukundo', 'Kicukiro');
INSERT INTO customers VALUES (5, 'Shema', 'Nyabihu');
INSERT INTO customers VALUES (6, 'Ruterana', 'Nyabihu');
INSERT INTO customers VALUES (7, 'Iduhorahafi', 'Remera');
INSERT INTO customers VALUES (8, 'Niyomugaba', 'Kimironko');
INSERT INTO customers VALUES (9, 'Uwase', 'Rubavu');
INSERT INTO customers VALUES (10, 'Uwera', 'Gakenke');
```
![My Project Screenshot](/screenshots/customers.png)

2. PRODUCTS TABLE
```sql
INSERT INTO products VALUES (1, 'Beans', 'Legumes');
INSERT INTO products VALUES (2, 'Oranges', 'Fruits');
INSERT INTO products VALUES (3, 'Carrots', 'Vegetables');
INSERT INTO products VALUES (4, 'Coffee', 'Cash Crops');
INSERT INTO products VALUES (5, 'Milk', 'Livestock');
INSERT INTO products VALUES (6, 'Flowers', 'Horticulture');
INSERT INTO products VALUES (7, 'Tea', 'Cash Crops');
INSERT INTO products VALUES (8, 'Onions', 'Vegetables');
INSERT INTO products VALUES (9, 'Bananas', 'Fruits');
INSERT INTO products VALUES (10, 'Rice', 'Cereals');
```
![My Project Screenshot](/screenshots/products.png)

3.TRANSACTIONS TABLE
```SQL
INSERT INTO transactions VALUES (1, 1, 1, '2025-01-03', 12000);
INSERT INTO transactions VALUES (2, 3, 4, '2025-04-13', 12400);
INSERT INTO transactions VALUES (3, 5, 7, '2025-05-09', 17800);
INSERT INTO transactions VALUES (4, 8, 2, '2025-09-09', 20000);
INSERT INTO transactions VALUES (5, 9, 8, '2025-07-03', 25000);
INSERT INTO transactions VALUES (6, 5, 4, '2025-02-20', 27000);
INSERT INTO transactions VALUES (7, 1, 9, '2025-03-15', 10000);
INSERT INTO transactions VALUES (8, 4, 8, '2025-01-10', 8000);
INSERT INTO transactions VALUES (9, 10, 1, '2025-01-10', 8000);
INSERT INTO transactions VALUES (10, 10, 10, '2025-10-10', 100000);
```
![My Project Screenshot](/screenshots/transactions1.png)





