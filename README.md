# E-Commerce Report and Analysis in Brazil: Sales Trends, Product Categories, and Consumer Behavior
## 📌 Project Overview
Brazilian E-Commerce Analysis, leveraging SQL for data processing and Power BI for visualization. This project examines transaction trends, payment behaviors, and product category performance based on 99,441 orders from 3,095 sellers across 71 product categories in Brazil.

## 📊 Data
**Source**          : [https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce](https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce)<br>
**Period**          : January 2017 - Juli 2018<br>
**Cleaned Dataset** : [Dataset](https://balikpapancerdas-my.sharepoint.com/:u:/g/personal/nurikarahmadani_mka_balikpapancerdas_id/EdhcxRLqQJVKuw9fGXXcY5sBkeQs363tfNv9dhfzJ0Js4g?e=7GhS3Q)

## 🎯 Objective
* Analyzed product distribution and pricing trends in Brazilian e-commerce.
* Identified patterns in payment methods and order statuses to optimize operational strategies.
* Provided actionable insights on product performance and customer satisfaction through reviews and delivery data.

## 🛠️ Methodology
* SQL: Data processing and cleansing.
* Power BI: Data visualization and creation of interactive dashboards.

## ⭐ Demonstrated skills
Data cleansing, data modeling, data visualization, and business analysis.

## 📈 Findings and Insights
### **Findings**
1. **Product Distribution & Categories**:
   - **Total Products**: **32,949 items** across **71 categories**.
   - **Categories with the Highest Product Count**: Include **bed_bath_table**, **sports_leisure**, and **furniture_decor**.
   - **Categories with the Highest Average Prices**: **Computers** and **musical_instruments**, while the lowest average prices are found in **books_general_interest** and **flowers**.
2. **Order Status**:
   - The majority of orders are marked as **delivered** (~97.02%), while smaller proportions fall into other statuses like **shipped**, **canceled**, and **invoiced**.
3. **Payment Methods**:
   - **Credit cards** dominate as the most frequently used payment method (75.24%), followed by **boleto** (23.41%) and other options like vouchers or debit cards.

4. **Order Geography**:
   - **São Paulo** is the region with the highest number of orders, followed by **Rio de Janeiro** and **Minas Gerais**.

5. **Delivery Efficiency**:
   - Late deliveries can be identified for further analysis to improve logistics processes.

6. **Product Reviews**:
   - Products with high and low ratings provide insights into customer satisfaction levels.

---

### **Insights**
1. **Sales Trends & Categories**:
   - Focusing on **computers** and **musical instruments** categories could yield higher margins due to their higher average prices.
   - Categories like **books** and **flowers** can attract budget-conscious customers.

2. **Payment Strategy**:
   - As the majority of users prefer **credit cards**, optimizing the credit card payment experience could enhance order conversion rates.

3. **Logistics Improvement**:
   - High-order regions like São Paulo require more efficient delivery strategies to avoid delays.

4. **Strengthening Product Reputation**:
   - Analyzing product reviews can help improve low-rated categories and leverage highly-rated products for promotional campaigns.

5. **Marketing Optimization**:
   - Location-based marketing campaigns could target regions with lower order counts to increase market penetration.

## 📊 Report
[Click here to view the interactive report in Power BI](https://app.powerbi.com/reportEmbed?reportId=389a9c4a-d470-44db-9d2a-c4c7bcf41c9f&autoAuth=true&ctid=ba657883-8e76-43e4-8134-c0d580d5fdea)

**Page 1**
![Brazilian E-Commerce - Publish_page-0001](https://github.com/user-attachments/assets/f4fb9dcc-802e-4b52-87d3-aefb35891aaf)

**Page 2**
![Brazilian E-Commerce - Publish_page-0002](https://github.com/user-attachments/assets/143b4beb-5dd3-414d-ab69-d0a3d7746f35)

## 📜 Steps And Details
## Database Preparation
```sql

--TABEL CUSTOMERS
CREATE DATABASE brazilian_ecommerce
CREATE TABLE customers(
  customer_id VARCHAR(100) PRIMARY KEY,
  customer_unique_id VARCHAR (100),
  customer_zip_code_prefix VARCHAR(100),
  customer_city VARCHAR(100),
  customer_state VARCHAR(100)
)
BULK INSERT customers
FROM 'C:\Users\NURIKA RAHMADANI\OneDrive - Balikpapan Cerdas\Data Analyst\Project\Brazilian E-Commerce Public Dataset by Olist\customers.csv'
WITH(
	FORMAT = 'CSV',
	FIRSTROW = 2,
	FIELDTERMINATOR = ',',
	ROWTERMINATOR = '\n',
	CODEPAGE = '1252'
)

--TABEL GEOLOCATIONS
CREATE TABLE geolocations(
	geolocation_zip_code VARCHAR (100),
	latitude VARCHAR(100),
	longitude VARCHAR(100),
	city VARCHAR(100),
	state VARCHAR(100)
)
BULK INSERT geolocations
FROM 'C:\Users\NURIKA RAHMADANI\OneDrive - Balikpapan Cerdas\Data Analyst\Project\Brazilian E-Commerce Public Dataset by Olist\geolocations.csv'
WITH(
	FORMAT = 'CSV',
	FIRSTROW = 2,
	FIELDTERMINATOR = ',',
	ROWTERMINATOR = '\n',
	CODEPAGE = '1252'
)

--TABEL ORDER_ITEMS
CREATE TABLE order_items(
	order_id VARCHAR (100),
	order_item_id VARCHAR(100),
	product_id VARCHAR(100),
	seller_id VARCHAR(100),
	shipping_limit_date DATETIME,
	price DECIMAL,
	freight_value VARCHAR(100),
)
BULK INSERT order_items
FROM 'C:\Users\NURIKA RAHMADANI\OneDrive - Balikpapan Cerdas\Data Analyst\Project\Brazilian E-Commerce Public Dataset by Olist\order_items.csv'
WITH(
	FORMAT = 'CSV',
	FIRSTROW = 2,
	FIELDTERMINATOR = ',',
	ROWTERMINATOR = '\n',
	CODEPAGE = '1252'
)

--TABEL ORDER_PAYMENTS
CREATE TABLE order_payments(
	order_id VARCHAR (100),
	payment_sequential VARCHAR(100),
	payment_type VARCHAR(100),
	payment_installments VARCHAR(100),
	payment_value DECIMAL
)
BULK INSERT order_payments
FROM 'C:\Users\NURIKA RAHMADANI\OneDrive - Balikpapan Cerdas\Data Analyst\Project\Brazilian E-Commerce Public Dataset by Olist\order_payments.csv'
WITH(
	FORMAT = 'CSV',
	FIRSTROW = 2,
	FIELDTERMINATOR = ',',
	ROWTERMINATOR = '\n',
	CODEPAGE = '1252'
)
--TABLE ORDER_REVIEWS
CREATE TABLE order_reviews(
	review_id VARCHAR (100),
	order_id VARCHAR(100),
	review_score INT,
	review_comment_title VARCHAR(100),
	review_comment_message VARCHAR(100),
	review_creation_date DATETIME,
	review_answer_timestamp DATETIME
)
BULK INSERT order_reviews
FROM 'C:\Users\NURIKA RAHMADANI\OneDrive - Balikpapan Cerdas\Data Analyst\Project\Brazilian E-Commerce Public Dataset by Olist\order_reviews.csv'
WITH(
	FORMAT = 'CSV',
	FIRSTROW = 2,
	FIELDTERMINATOR = ',',
	ROWTERMINATOR = '\n',
	CODEPAGE = '1252'
)

--TABEL PRODUCT_CATEGORY
CREATE TABLE products_category(
  product_category_name VARCHAR(100),
  product_category_name_english VARCHAR (100),

)
BULK INSERT products_category
FROM 'C:\Users\NURIKA RAHMADANI\OneDrive - Balikpapan Cerdas\Data Analyst\Project\Brazilian E-Commerce Public Dataset by Olist\product_category.csv'
WITH(
	FORMAT = 'CSV',
	FIRSTROW = 2,
	FIELDTERMINATOR = ',',
	ROWTERMINATOR = '\n',
	CODEPAGE = '1252'
)

-TABEL PRODUCTS

CREATE TABLE products(
  product_id VARCHAR(100) PRIMARY KEY,
  product_category_name VARCHAR (100),
  product_name_lenght DECIMAL,
  product_description_lenght DECIMAL,
  product_photos_qty DECIMAL,
  product_weight_g DECIMAL,
  product_length_cm DECIMAL,
  product_height_cm DECIMAL,
  product_width_cm DECIMAL
)
BULK INSERT products
FROM 'C:\Users\NURIKA RAHMADANI\OneDrive - Balikpapan Cerdas\Data Analyst\Project\Brazilian E-Commerce Public Dataset by Olist\products.csv'
WITH(
	FORMAT = 'CSV',
	FIRSTROW = 2,
	FIELDTERMINATOR = ',',
	ROWTERMINATOR = '\n',
	CODEPAGE = '1252'
)

--TABLE SELLERS

CREATE TABLE sellers(
  seller_id VARCHAR(100) PRIMARY KEY,
  seller_zip_code_prefix VARCHAR (100),
  seller_city VARCHAR(100),
  seller_state VARCHAR(100)
)
BULK INSERT sellers
FROM 'C:\Users\NURIKA RAHMADANI\OneDrive - Balikpapan Cerdas\Data Analyst\Project\Brazilian E-Commerce Public Dataset by Olist\sellers.csv'
WITH(
	FORMAT = 'CSV',
	FIRSTROW = 2,
	FIELDTERMINATOR = ',',
	ROWTERMINATOR = '\n',
	CODEPAGE = '1252'
)
--TABEL ORDERS
CREATE TABLE orders(
	order_id VARCHAR(100),
	customer_id VARCHAR(100),
	order_status VARCHAR(100),
	order_purchase_timestamp VARCHAR(100),
	order_approved_at VARCHAR(100),
	order_delivered_carrier_date DATETIME,
	order_delivered_customer_date DATETIME,
	order_estimated_delivery_date DATETIME
)
BULK INSERT orders
FROM 'C:\Users\NURIKA RAHMADANI\OneDrive - Balikpapan Cerdas\Data Analyst\Project\Brazilian E-Commerce Public Dataset by Olist\orders.csv'
WITH(
	FORMAT = 'CSV',
	FIRSTROW = 2,
	FIELDTERMINATOR = ',',
	ROWTERMINATOR = '\n',
	CODEPAGE = '1252'
)
```
## Data Cleaning and Normalization
```sql
-- Mengecek null values
SELECT * FROM customers
WHERE
	customer_id IS NULL
	OR customer_unique_id IS NULL
	OR customer_zip_code_prefix IS NULL
	OR customer_city IS NULL
	OR customer_state IS NULL
-- no null data

SELECT 
    customer_id, 
    COUNT(*) AS Jumlah
FROM customers
GROUP BY customer_id
HAVING COUNT(*) > 1;
--no duplicate value

--duplicate value
WITH CTE_Duplikat AS (
    SELECT *, 
	ROW_NUMBER() OVER (PARTITION BY customer_unique_id ORDER BY customer_id) AS Row_Num
    FROM customers
)
DELETE FROM CTE_Duplikat
WHERE Row_Num > 1;

--TABEL GEOLOCATIONS
SELECT * FROM geolocations
WHERE
	geolocation_zip_code IS NULL
	OR latitude IS NULL
	OR latitude IS NULL
	OR city IS NULL
	OR state IS NULL

-- Menambahkan kolom baru ke tabel products
ALTER TABLE products
ADD product_category_name_english NVARCHAR(255);

-- Memperbarui data di kolom baru menggunakan data dari tabel products_category
UPDATE p
SET p.product_category_name_english = pc.product_category_name_english
FROM products AS p
JOIN products_category AS pc
ON p.product_category_name = pc.product_category_name;


ALTER TABLE orders
ADD order_years VARCHAR(20)
UPDATE orders
SET order_years = YEAR(order_purchase_timestamp)

UPDATE geolocations SET state = 'Acre' WHERE state = 'AC';
UPDATE geolocations SET state = 'Alagoas' WHERE state = 'AL';
UPDATE geolocations SET state = 'Amapá' WHERE state = 'AP';
UPDATE geolocations SET state = 'Amazonas' WHERE state = 'AM';
UPDATE geolocations SET state = 'Bahia' WHERE state = 'BA';
UPDATE geolocations SET state = 'Ceará' WHERE state = 'CE';
UPDATE geolocations SET state = 'Distrito Federal' WHERE state = 'DF';
UPDATE geolocations SET state = 'Espírito Santo' WHERE state = 'ES';
UPDATE geolocations SET state = 'Goiás' WHERE state = 'GO';
UPDATE geolocations SET state = 'Maranhão' WHERE state = 'MA';
UPDATE geolocations SET state = 'Mato Grosso' WHERE state = 'MT';
UPDATE geolocations SET state = 'Mato Grosso do Sul' WHERE state = 'MS';
UPDATE geolocations SET state = 'Minas Gerais' WHERE state = 'MG';
UPDATE geolocations SET state = 'Pará' WHERE state = 'PA';
UPDATE geolocations SET state = 'Paraíba' WHERE state = 'PB';
UPDATE geolocations SET state = 'Paraná' WHERE state = 'PR';
UPDATE geolocations SET state = 'Pernambuco' WHERE state = 'PE';
UPDATE geolocations SET state = 'Piauí' WHERE state = 'PI';
UPDATE geolocations SET state = 'Rio de Janeiro' WHERE state = 'RJ';
UPDATE geolocations SET state = 'Rio Grande do Norte' WHERE state = 'RN';
UPDATE geolocations SET state = 'Rio Grande do Sul' WHERE state = 'RS';
UPDATE geolocations SET state = 'Rondônia' WHERE state = 'RO';
UPDATE geolocations SET state = 'Roraima' WHERE state = 'RR';
UPDATE geolocations SET state = 'Santa Catarina' WHERE state = 'SC';
UPDATE geolocations SET state = 'São Paulo' WHERE state = 'SP';
UPDATE geolocations SET state = 'Sergipe' WHERE state = 'SE';
UPDATE geolocations SET state = 'Tocantins' WHERE state = 'TO';

ALTER TABLE orders
ALTER COLUMN order_id VARCHAR(100) NOT NULL;
ALTER TABLE orders
ADD CONSTRAINT order_id PRIMARY KEY (order_id);

--menambahkan foreign key di order_items. tapi ternyata terdapat data di order_items yang tidak ada di tabel parent orders(mismatch value)
--mengecek apakah ada mismacth value denga query ini
SELECT DISTINCT product_id
FROM order_items
WHERE product_id NOT IN (
    SELECT product_id
    FROM products
);
DELETE FROM order_items
WHERE product_id NOT IN (
    SELECT product_id
    FROM products
);
ALTER TABLE order_items
ADD CONSTRAINT fk_product_id FOREIGN KEY(product_id)
REFERENCES products(product_id)

SELECT DISTINCT order_id
FROM order_payments
WHERE order_id NOT IN (
    SELECT order_id
    FROM orders
);
DELETE FROM order_payments
WHERE order_id NOT IN (
    SELECT order_id
    FROM orders
);
ALTER TABLE order_payments
ADD CONSTRAINT fk_order_payments FOREIGN KEY(order_id)
REFERENCES orders(order_id)

--menambahkan primary key namun terdapat duplikat value
SELECT review_id, COUNT(*)
FROM order_reviews
GROUP BY review_id
HAVING COUNT(*) > 1;

DELETE FROM order_reviews
WHERE review_id IN (
    SELECT review_id
    FROM order_reviews
    GROUP BY review_id
    HAVING COUNT(*) > 1
);
ALTER TABLE order_reviews
ADD CONSTRAINT review_id PRIMARY KEY(review_id)

--menambahkan foreign key
SELECT DISTINCT order_id
FROM order_reviews
WHERE order_id NOT IN (
    SELECT order_id
    FROM orders
);
DELETE FROM order_reviews
WHERE order_id NOT IN (
    SELECT order_id
    FROM orders
);
ALTER TABLE order_reviews
ADD CONSTRAINT fk_order_reviews FOREIGN KEY(order_id)
REFERENCES orders(order_id)

--relasi customers dengan orders

--MENAMBAHKAN KOLOM PRICE PADA TABEL PRODUCT
UPDATE p
SET p.price = oi.price
FROM products p
JOIN order_items oi ON p.product_id = oi.product_id
WHERE p.price IS NULL;

--MENGGANTI NULL PADA KATEGORI MENJADI 'OTHERS'
UPDATE products
SET product_category_name_english = 'Others'
WHERE product_category_name_english IS NULL
```

## Find Outliers
```sql
-- order_items table
SELECT *
FROM order_items
WHERE 
    ABS(price - 120.701189) > 3 * 184;  -- 3 standar deviasi dari rata-rata
```

## ANALYSIS
### TABEL ORDERS
```SQL
select * from orders

select distinct order_status from orders

select * from orders
where order_status = 'canceled'

--MENCARI ORDERS YANG TERLAMBAT DIKIRIM
SELECT order_id, order_delivered_customer_date, order_estimated_delivery_date,
       DATEDIFF(DAY, order_delivered_customer_date, order_estimated_delivery_date) AS selisih
FROM orders
WHERE DATEDIFF(DAY, order_delivered_customer_date, order_estimated_delivery_date) < 0;
```
### Banyak order untuk tiap seller
```sql
SELECT 
    oi.seller_id,
    COUNT(o.order_id) AS order_counts
FROM order_items oi
INNER JOIN orders o ON oi.order_id = o.order_id
GROUP BY oi.seller_id;
```
### menampilkan data jumlah customer berdasarkan state
```SQL
--menampilkan data jumlah customer berdasarkan state

SELECT 
	COUNT(*) as customer_counts,
	customer_state
FROM customers
GROUP BY customer_state
ORDER BY customer_counts DESC
```

### menampilkan customer dengan jumlah orderan terbanyak
```sql

SELECT 
	COUNT(order_id) as order_count,
	customer_id
FROM orders
GROUP BY customer_id
ORDER BY order_count DESC

--turns out masing masing customer hanya order 1 kali dalam dataset ini
```
### ingn menambahkan total transaksi ke dalam tabel orders
```sql
--ingn menambahkan total transaksi ke dalam tabel orders
--dimana nominal price terdapat pada tabel order items
 
ALTER TABLE orders
ADD total_transaction DECIMAL

--menggunakan subquery dengan nama "agg"
UPDATE o
SET o.total_transaction = agg.total_price
FROM orders o
JOIN (
    SELECT order_id, SUM(price) AS total_price
    FROM order_items
    GROUP BY order_id
) agg ON o.order_id = agg.order_id;
```
### customer dengan total transaksi terbanyak
```SQL
--customer dengan total transaksi terbanyak

SELECT TOP 5 *
FROM orders
ORDER BY total_transaction DESC
```
### mencari jumlah produk yang diorder berdasarkan kategori barang
```SQL

--mencari jumlah produk yang diorder berdasarkan kategori barang
--berarti butuh tabel order_items dan products

SELECT 
	COUNT(o.product_id) as product_count,
	p.product_category_name_english as category
FROM order_items o
JOIN products p ON p.product_id = o.product_id
GROUP BY p.product_category_name_english 
ORDER BY product_count DESC
```
### analisis harga produk
```sql
--menghitung rata rata harga item
SELECT 
	AVG(price) as average_price
FROM products


--menghitung rata rata harga produk untuk tiap kategori
SELECT 
	AVG(price) as average_price,
	product_category_name_english as product_category
FROM products
GROUP BY product_category_name_english
```
### analisis banyak orderan
```sql
--menghitung banyak orderan berdasarkan statusnya
SELECT 
	count(*) as order_count,
	order_status
FROM orders
GROUP BY order_status

--menghitung banyak orderan berdasarkan tahun
SELECT 
	count(*) as order_count,
	YEAR(order_purchase_timestamp) AS years
FROM orders
GROUP BY YEAR(order_purchase_timestamp)

--Menampilkan banyak orderan berdasarkan payment method
SELECT 
	COUNT(*) as order_count,
	payment_type
FROM order_payments
GROUP BY payment_type
```
### Analisis Review 
```sql

--Menampilkan banyak review per review score
SELECT 
	COUNT(*) total_review,
	review_score
FROM order_reviews
GROUP BY review_score
ORDER BY review_score

--Menampilkan rata rata review score per product kategori
SELECT 
	AVG(orv.review_score) as average_review_score,
	p.product_category_name_english as product_category
FROM order_reviews orv
JOIN order_items  ort ON orv.order_id = ort.order_id
JOIN products p ON ort.product_id = p.product_id
GROUP BY p.product_category_name_english
ORDER BY average_review_score DESC
```


