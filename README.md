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
--TABLE ORDER_REVIEWS-----MASIH EROR
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
	ROWTERMINATOR = '\r\n',
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




```
