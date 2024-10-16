# Store-DB-.-
CREATE DATABASE online_store;
USE online_store;

CREATE TABLE stores (
    store_code VARCHAR(10) PRIMARY KEY,
    store_name VARCHAR(100),
    store_url VARCHAR(255),
    store_country VARCHAR(50),
    phone VARCHAR(20),
    email VARCHAR(100),
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

CREATE TABLE transactions (
    transaction_id INT AUTO_INCREMENT PRIMARY KEY,
    store_code VARCHAR(10),
    transaction_type VARCHAR(50),
    amount DECIMAL(10, 2),
    total DECIMAL(10, 2),
    tax DECIMAL(10, 2),
    error_code VARCHAR(20),
    ip_address VARCHAR(45),
    postal_code VARCHAR(20),
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    FOREIGN KEY (store_code) REFERENCES stores(store_code)
);

CREATE TABLE customers (
    customer_id INT AUTO_INCREMENT PRIMARY KEY,
    customer_name VARCHAR(100),
    credit_card_num VARCHAR(20),
    credit_card_date VARCHAR(7),  -- Формат: MM/YYYY
    credit_card_cvv VARCHAR(4),
    billing_country VARCHAR(50),
    billing_city VARCHAR(50),
    state_province VARCHAR(50),
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

CREATE TABLE products (
    product_id INT AUTO_INCREMENT PRIMARY KEY,
    product_name VARCHAR(100),
    visible BOOLEAN,
    weight DECIMAL(10, 2),
    height DECIMAL(10, 2),
    sold INT,
    currency VARCHAR(5),
    price DECIMAL(10, 2),
    image_url VARCHAR(255),
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

CREATE TABLE orders (
    order_id INT AUTO_INCREMENT PRIMARY KEY,
    customer_id INT,
    transaction_id INT,
    order_date TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    shipping_cost DECIMAL(10, 2),
    quantity INT,
    status VARCHAR(50),
    notes TEXT,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    FOREIGN KEY (customer_id) REFERENCES customers(customer_id),
    FOREIGN KEY (transaction_id) REFERENCES transactions(transaction_id)
);

CREATE TABLE products (
    store_id INTEGER NOT NULL,
    product_id INTEGER PRIMARY KEY AUTOINCREMENT,
    visible TINYINT NOT NULL DEFAULT 1,
    height INTEGER NULL,
    weight INTEGER NULL,
    currency VARCHAR(3) NULL,
    price DECIMAL(9, 3) NULL,
    product_name VARCHAR(50) NOT NULL,
    sold INTEGER NULL,
    image_url VARCHAR(255) NULL,
    notes VARCHAR(255) NULL,
    quality INTEGER NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

    INSERT INTO products (store_id, visible, height, weight, currency, price, product_name, sold, image_url, notes, quality, created_at)
    -> VALUES
    -> (1, 1, 20, 500, 'UAH', 19.50, 'Bread', 250, 'https://www.jabko/image/bread.jpg', 'The promotion is valid until 15.10.2024', 300, '2024-10-13 12:17:51'),
    -> (1, 1, 15, 300, 'UAH', 25.00, 'Milk', 150, 'https://www.jabko/image/milk.jpg', 'Fresh product', 250, '2024-10-13 12:17:51'),
    -> (1, 1, 10, 1000, 'UAH', 12.30, 'Flour', 75, 'https://www.jabko/image/flour.jpg', 'Suitable for baking', 400, '2024-10-13 12:17:51'),
    -> (1, 1, 30, 200, 'UAH', 12.30, 'Butter', 180, 'https://www.jabko/image/butter.jpg', 'Best before 20.10.2024', 320, '2024-10-13 12:17:51'),
    -> (1, 1, 5, 50, 'UAH', 7.80, 'Eggs', 500, 'https://www.jabko/image/eggs.jpg', 'Pack of 10', 290, '2024-10-13 12:17:51'),
    -> (1, 1, 15, 600, 'UAH', 35.60, 'Cheese', 100, 'https://www.jabko/image/cheese.jpg', 'Aged 3 months', 350, '2024-10-13 12:17:51'),
    -> (1, 1, 18, 700, 'UAH', 60.00, 'Chicken', 600, 'https://www.jabko/image/chicken.jpg', 'Organic meat', 280, '2024-10-13 12:17:51'),
    -> (1, 1, 12, 400, 'UAH', 17.80, 'Rice', 40, 'https://www.jabko/image/rice.jpg', 'Long grain variety', 260, '2024-10-13 12:17:51'),
    -> (1, 1, 9, 400, 'UAH', 29.50, 'Apples', 220, 'https://www.jabko/image/apples.jpg', 'Golden variety', 310, '2024-10-13 12:17:51'),
    -> (1, 1, 12, 450, 'UAH', 14.00, 'Tomatoes', 180, 'https://www.jabko/image/tomatoes.jpg', 'Greenhouse grown', 260, '2024-10-13 12:17:51'),
    -> (1, 1, 25, 300, 'UAH', 45.00, 'Oranges', 150, 'https://www.jabko/image/oranges.jpg', 'Sweet and juicy', 290, '2024-10-13 12:17:51'),
    -> (1, 1, 10, 250, 'UAH', 9.99, 'Potatoes', 400, 'https://www.jabko/image/potatoes.jpg', 'Freshly harvested', 350, '2024-10-13 12:17:51'),
    -> (1, 1, 20, 600, 'UAH', 35.00, 'Grapes', 220, 'https://www.jabko/image/grapes.jpg', 'Seedless grapes', 380, '2024-10-13 12:17:51'),
    -> (1, 1, 15, 400, 'UAH', 2.50, 'Carrots', 350, 'https://www.jabko/image/carrots.jpg', 'Rich in vitamins', 280, '2024-10-13 12:17:51'),
    -> (1, 1, 8, 300, 'UAH', 7.00, 'Lettuce', 500, 'https://www.jabko/image/lettuce.jpg', 'Crispy and fresh', 320, '2024-10-13 12:17:51'),
    -> (1, 1, 18, 700, 'UAH', 19.99, 'Bananas', 500, 'https://www.jabko/image/bananas.jpg', 'Rich in potassium', 260, '2024-10-13 12:17:51');
