
# 🧹 E-commerce Data Cleaning & KPI Analysis (SQL Project)

This project demonstrates how to clean, transform, and analyze raw e-commerce data using SQL in **MySQL Workbench**. The goal is to prepare structured, clean datasets and extract business insights through key performance indicators (KPIs).

---

## 📁 Datasets Used

Three CSV files were used as raw input data:

- `customers_raw.csv`
- `orders_raw.csv`
- `products_raw.csv`

---

## 🧠 Project Goals

- Clean and format raw customer, order, and product data.
- Handle missing values, incorrect formats, and inconsistent records.
- Join the cleaned tables into a single unified view (`ecommerce_full_view`).
- Derive business KPIs using SQL.
- Export cleaned data for further analysis or visualization.

---

## 🔨 Tools Used

- **MySQL Workbench**
- **SQL**
- **CSV files**
- *(Optional visualization tools: Excel / Tableau / Power BI)*

---

## 🧹 Step-by-Step Cleaning Process

### 1. Customers Cleaning (`customers_clean`)
- Removed duplicate and invalid entries.
- Standardized names to proper case.
- Reformatted signup dates to `YYYY-MM-DD`.
- Cleaned phone numbers by removing special characters.
- Removed records with missing or invalid emails.

### 2. Orders Cleaning (`orders_clean`)
- Converted `order_date` to proper date format.
- Removed records with missing product IDs or total_price < 0.
- Handled null values.

### 3. Products Cleaning (`products_clean`)
- Removed records with missing name or category.
- Converted product names and categories to proper case.
- Ensured valid prices (price > 0).

---

## 🔗 Data Joining

Created a unified view `ecommerce_full_view` by joining:
- `orders_clean`
- `customers_clean`
- `products_clean`

```sql
SELECT
  o.order_id,
  o.order_date,
  c.customer_id,
  c.name AS customer_name,
  c.email,
  p.product_id,
  p.name AS product_name,
  p.category,
  o.quantity,
  o.total_price
FROM orders_clean o
JOIN customers_clean c ON o.customer_id = c.customer_id
JOIN products_clean p ON o.product_id = p.product_id;
```

---

## 📊 Business KPIs (Insights)

### ✅ Total Revenue
```sql
SELECT SUM(total_price) AS total_revenue FROM ecommerce_full_view;
```

### ✅ Total Orders
```sql
SELECT COUNT(DISTINCT order_id) AS total_orders FROM ecommerce_full_view;
```

### ✅ Unique Customers
```sql
SELECT COUNT(DISTINCT customer_id) AS unique_customers FROM ecommerce_full_view;
```

### ✅ Average Order Value (AOV)
```sql
SELECT AVG(total_price) AS average_order_value FROM ecommerce_full_view;
```

### ✅ Top 10 Products by Sales
```sql
SELECT p.name AS product_name, SUM(o.total_price) AS total_sales
FROM ecommerce_full_view o
JOIN products_clean p ON o.product_id = p.product_id
GROUP BY p.name
ORDER BY total_sales DESC
LIMIT 10;
```

### ✅ Revenue by Category
```sql
SELECT p.category, SUM(o.total_price) AS revenue_by_category
FROM ecommerce_full_view o
JOIN products_clean p ON o.product_id = p.product_id
GROUP BY p.category
ORDER BY revenue_by_category DESC;
```

---

## 📤 Exported Files

The following cleaned and transformed files were exported:
- `ecommerce_full_view.csv`
- `customers_clean.csv`
- `orders_clean.csv`
- `products_clean.csv`

---

## 📈 Insights & Summary

- The top-selling products generated the majority of revenue.
- Electronics and fashion were the most profitable categories.
- Average order value provides insight into customer spending habits.
- The cleaned dataset can now be used for reporting, dashboards, or forecasting.

---

## 📌 Resume Summary

> **E-commerce Data Cleaning & KPI Analysis | SQL, MySQL Workbench**  
> Cleaned and transformed raw customer, order, and product data using SQL. Joined datasets into a unified view and calculated business KPIs such as total revenue, AOV, and top products. Exported results for further analysis.

---

## 📎 License

This project is for educational and portfolio use only.
