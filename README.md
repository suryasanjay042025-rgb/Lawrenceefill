
CREATE DATABASE lawrence_enterprise;
USE lawrence_enterprise;

CREATE TABLE admins (
 id INT AUTO_INCREMENT PRIMARY KEY,
 username VARCHAR(100),
 password VARCHAR(255)
);

INSERT INTO admins (username,password)
VALUES ('admin','admin123');

CREATE TABLE products (
 id INT AUTO_INCREMENT PRIMARY KEY,
 name VARCHAR(200),
 price DECIMAL(10,2),
 stock INT
);

CREATE TABLE cart (
 id INT AUTO_INCREMENT PRIMARY KEY,
 product_id INT,
 qty INT
);

CREATE TABLE orders (
 id INT AUTO_INCREMENT PRIMARY KEY,
 total DECIMAL(10,2),
 status VARCHAR(50) DEFAULT 'Pending'
);

CREATE TABLE repairs (
 id INT AUTO_INCREMENT PRIMARY KEY,
 tracking_id VARCHAR(50),
 customer_name VARCHAR(150),
 phone VARCHAR(50),
 device VARCHAR(150),
 issue TEXT,
 status VARCHAR(100) DEFAULT 'Received'
);
