CREATE TABLE student (
    student_id INT PRIMARY KEY,
    first_name VARCHAR(30),
    last_name VARCHAR(30),
    age INT,
    department VARCHAR(20),
    points INT,
    city VARCHAR(30)
);
CREATE TABLE product (
    product_id INT PRIMARY KEY,
    product_name VARCHAR(30),
    price DECIMAL(10,2),
    quantity INT
);

INSERT INTO student
(student_id, first_name, last_name, age, department, points, city)
VALUES
(1, 'Abu', 'Sayed', 20, 'CSE', 8, 'Dhaka'),
(2, 'Abrar', 'Fahad', 22, 'EEE', 7, 'Chittagong'),
(3, 'Felani', 'Khatun', 21, 'CSE', NULL, 'Dhaka'),
(4, 'Shahinur', 'Begum', 23, 'BBA', 6, 'Khulna'),
(5, 'Osman', 'Hadi', 20, 'CSE', 9, 'Rajshahi'),
(6, 'Hrida', 'Akter', 22, 'EEE', 5, NULL);
INSERT INTO product
(product_id, product_name, price, quantity)
VALUES
(1, 'Laptop', 80000, 5),
(2, 'Mouse', 500, 50),
(3, 'Keyboard', 1500, NULL),
(4, 'Monitor', 12000, 10),
(5, 'Printer', 20000, 2);
