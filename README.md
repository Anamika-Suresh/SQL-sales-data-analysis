# Sales Data Analysis - SQL & Power BI

An end-to-end sales data analysis project using **SQL (SQLite/MySQL)** for data extraction and **Microsoft Power BI** for business intelligence reporting. 

Additionally, this repository contains a modern **Interactive Dashboard Preview** written in HTML, CSS, and Chart.js to explore the analysis results in any browser.

---

## SQL Data Analysis Queries & Insights

The data analysis was performed on the database dump containing transactional records. Below are the key queries and their findings:

### 1. Show all customer records
```sql
SELECT * FROM customers;
```
* **Insight:** Total of **38 active customer accounts** consisting of Brick & Mortar stores and E-Commerce platforms.

### 2. Show total number of customers
```sql
SELECT count(*) FROM customers;
-- Result: 38
```

### 3. Show transactions for Chennai market
```sql
SELECT * FROM transactions where market_code='Mark001';
```
* **Insight:** There are **1,028 transactions** recorded specifically in the Chennai market (Market Code: `Mark001`).

### 4. Show distinct product codes sold in Chennai
```sql
SELECT distinct product_code FROM transactions where market_code='Mark001';
```
* **Insight:** A total of **76 unique products** were sold to customers in Chennai.

### 5. Show transactions where currency is US dollars
```sql
SELECT * from transactions where currency="USD";
```
* **Insight:** Found **2 transactions** totaling **$750 USD** (under customer `Cus005` in market `Mark004`).

### 6. Show total revenue in year 2020
```sql
SELECT SUM(transactions.sales_amount) 
FROM transactions 
INNER JOIN date ON transactions.order_date=date.date 
WHERE date.year=2020 and (transactions.currency="INR" or transactions.currency="USD");
-- Result: ₹142,224,545 (142.22M INR)
```

### 7. Show total revenue in year 2020, January Month
```sql
SELECT SUM(transactions.sales_amount) 
FROM transactions 
INNER JOIN date ON transactions.order_date=date.date 
WHERE date.year=2020 and date.month_name="January" and (transactions.currency="INR" or transactions.currency="USD");
-- Result: ₹25,656,567 (25.66M INR)
```

### 8. Show total revenue in year 2020 in Chennai market
```sql
SELECT SUM(transactions.sales_amount) 
FROM transactions 
INNER JOIN date ON transactions.order_date=date.date 
WHERE date.year=2020 and transactions.market_code="Mark001";
-- Result: ₹2,463,024 (2.46M INR)
```

---

##  Local Interactive Dashboard Preview
We developed an interactive web preview of the sales dashboard using modern glassmorphic styling and Chart.js.

### How to Run Locally:
1. Clone this repository.
2. Launch a local web server in the directory:
   ```bash
   python -m http.server 8000
   ```
3. Open your browser and navigate to `http://localhost:8000/dashboard.html`.

### Features:
* **Interactive KPIs:** Dynamically computed sales metrics for the year 2020, Chennai market, active customers, and USD records.
* **Rich Charts:** Interactive visual representation of YoY Revenue, Monthly Trend, Market Revenue Share, and Customer Contribution.
* **SQL Console:** A reference section containing all analytical SQL queries and their calculated answers.
* **Power BI Screenshots:** Slideshow gallery showing the actual reports from Power BI Desktop.
* **Responsive Dark/Light Mode:** Full user interface support for dark and light theme styles.

---

## Power BI Dashboards
The Power BI Desktop file [Sales-Data-Analysis.pbix](Sales-Data-Analysis.pbix) has been designed with three primary pages:
1. **Key Insights:** High-level executive overview of sales numbers, customer contribution, and revenue trend.
2. **Profit Analysis:** Deep dive into product margins, cost structures, and market profitability.
3. **Performance Insights:** Performance metrics mapped to target goals and historical trends.

---

## Database Structure
The project database layout comprises the following tables:
* `customers`: Active clients, categorized by retail type (Brick & Mortar / E-Commerce).
* `markets`: Operational distribution hubs across different regions/zones (North, Central, South).
* `products`: Listing of active product codes.
* `date`: Time intelligence calendar mapping dates to calendar years and months.
* `transactions`: Transaction ledger records representing product sales qty, amount, margins, and currency.
