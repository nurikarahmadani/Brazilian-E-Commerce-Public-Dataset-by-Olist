# Brazilian-E-Commerce-Public-Dataset-by-Olist

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
