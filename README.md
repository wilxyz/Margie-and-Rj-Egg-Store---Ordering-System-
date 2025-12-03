<div align="center" style="padding-top: 5px">

<img src="" width="300" height="300"/>

## Margie and Rj Egg Store
*Fresh Eggs Daily!*

**Margie & RJ Egg Store** *is a family-run supplier offering fresh, carefully handled eggs for households and small businesses. We focus on consistent quality, prompt pickup or delivery, and honest, community-centered service.*

</div>

## Pre-requites

- *Node.js (LTS recommended)*
- *XAMPP* (Apache + MySQL/MariaDB)
- *Visual Studio Code or another IDE that has an integrated terminal*

## How to Run and Execute the File

**Verify Node js**
```bash
# check Node and npm
node -v
npm -v
```
- *If not installed, download and install from `https://nodejs.org/` (choose LTS)

## Start XAMPP and Open PhpMyAdmin

- *Open XAMPP Control Panel.*
- *Start Apache and MySQL.*
- *Click Admin next to MySQL to open phpMyAdmin.*

## Create Database
- *In PhpMyAdmin, create a database*
```bash
CREATE DATABASE egg_trading;
```

## Create Tables 
- *With `egg_trading` selected, open the SQL tab and run the following schema.*
```bash
CREATE TABLE users (
  id INT(11) NOT NULL AUTO_INCREMENT,
  username VARCHAR(50) COLLATE utf8_general_ci NOT NULL,
  email VARCHAR(100) COLLATE utf8_general_ci NOT NULL,
  password VARCHAR(255) COLLATE utf8_general_ci NOT NULL,
  google_id VARCHAR(255) COLLATE utf8_general_ci DEFAULT NULL,
  password_reset_token VARCHAR(255) COLLATE utf8_general_ci DEFAULT NULL,
  created_at TIMESTAMP NOT NULL DEFAULT CURRENT_TIMESTAMP,
  otp VARCHAR(6) COLLATE utf8_general_ci DEFAULT NULL,
  otp_expiry BIGINT(20) DEFAULT NULL,
  PRIMARY KEY (id)
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COLLATE=utf8_general_ci;

CREATE TABLE IF NOT EXISTS orders (
  id INT AUTO_INCREMENT PRIMARY KEY,
  user_id INT NOT NULL,
  total_amount DECIMAL(10,2) NOT NULL,
  pickup_date DATE NOT NULL,
  pickup_time TIME NOT NULL,
  name VARCHAR(100) NOT NULL,
  phone VARCHAR(30) NOT NULL,
  address TEXT NOT NULL,
  notes TEXT,
  status ENUM('placed','cancelled') DEFAULT 'placed',
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
  FOREIGN KEY (user_id) REFERENCES users(id) ON DELETE CASCADE
);

CREATE TABLE IF NOT EXISTS order_items (
  id INT AUTO_INCREMENT PRIMARY KEY,
  order_id INT NOT NULL,
  product_name VARCHAR(100) NOT NULL,
  size VARCHAR(50) NOT NULL,
  price DECIMAL(10,2) NOT NULL,
  quantity INT NOT NULL,
  subtotal DECIMAL(10,2) NOT NULL,
  FOREIGN KEY (order_id) REFERENCES orders(id) ON DELETE CASCADE
);
```






