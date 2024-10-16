# Store-DB-.-
CREATE TABLE stores (
    store_code VARCHAR(50) PRIMARY KEY,
    store_name VARCHAR(100),
    store_url VARCHAR(100),
    store_country VARCHAR(50),
    phone VARCHAR(15),
    email VARCHAR(100),
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

CREATE TABLE customers (
    customer_id SERIAL PRIMARY KEY,
    customer_name VARCHAR(100),
    billing_country VARCHAR(50),
    billing_city VARCHAR(50),
    state_province VARCHAR(50),
    postal_code VARCHAR(20),
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

CREATE TABLE orders (
    order_id SERIAL PRIMARY KEY,
    store_code VARCHAR(50),
    customer_id INT,
    order_date TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    payment_status VARCHAR(20),
    total DECIMAL(10, 2),
    shipping_cost DECIMAL(10, 2),
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    FOREIGN KEY (store_code) REFERENCES stores(store_code),
    FOREIGN KEY (customer_id) REFERENCES customers(customer_id)
);

CREATE TABLE transactions (
    transaction_id SERIAL PRIMARY KEY,
    order_id INT,
    transaction_type VARCHAR(20),
    amount DECIMAL(10, 2),
    tax DECIMAL(10, 2),
    error_code VARCHAR(20),
    ip_address VARCHAR(15),
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    FOREIGN KEY (order_id) REFERENCES orders(order_id)
);

CREATE TABLE products (
    product_id SERIAL PRIMARY KEY,
    store_code VARCHAR(50),
    product_name VARCHAR(100),
    visible BOOLEAN,
    weight DECIMAL(10, 2),
    height DECIMAL(10, 2),
    sold INT,
    currency VARCHAR(10),
    price DECIMAL(10, 2),
    image_url VARCHAR(255),
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    FOREIGN KEY (store_code) REFERENCES stores(store_code)
);

CREATE TABLE order_items (
    order_item_id SERIAL PRIMARY KEY,
    order_id INT,
    product_id INT,
    quantity INT,
    notes TEXT,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    FOREIGN KEY (order_id) REFERENCES orders(order_id),
    FOREIGN KEY (product_id) REFERENCES products(product_id)
);
INSERT INTO products (store_id, visible, height, weight, currency, price, product_name, sold, image_url, notes, quality, created_at) VALUES
    -> (1, 1, 270, 700, 'UA', 45.000, 'Rice', 40, 'https://www.jabko/image/rice.jpg', 'Довгозерний сорт', 1, '2024-10-13 12:17:51'),
    -> (1, 1, 310, 400, 'UA', 29.500, 'Apples', 220, 'https://www.jabko/image/apples.jpg', 'Золотий сорт', 1, '2024-10-13 12:17:51'),
    -> (1, 1, 260, 200, 'UA', 14.000, 'Tomatoes', 180, 'https://www.jabko/image/tomatoes.jpg', 'Вирощено в теплиці', 1, '2024-10-13 12:17:51'),
    -> (1, 1, 500, 1500, 'UA', 85.500, 'Potatoes', 350, 'https://www.jabko/image/potatoes.jpg', 'Свіжі картоплі', 1, '2024-10-13 12:17:51'),
    -> (1, 1, 200, 300, 'UA', 22.000, 'Carrots', 120, 'https://www.jabko/image/carrots.jpg', 'Органічні моркви', 1, '2024-10-13 12:17:51'),
    -> (1, 1, 400, 600, 'UA', 15.000, 'Cabbage', 80, 'https://www.jabko/image/cabbage.jpg', 'Вітамінний продукт', 1, '2024-10-13 12:17:51'),
    -> (1, 1, 150, 450, 'UA', 10.500, 'Grapes', 200, 'https://www.jabko/image/grapes.jpg', 'Свіжі виногради', 1, '2024-10-13 12:17:51'),
    -> (1, 1, 350, 700, 'UA', 28.900, 'Oranges', 150, 'https://www.jabko/image/oranges.jpg', 'Солодкі апельсини', 1, '2024-10-13 12:17:51');

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
