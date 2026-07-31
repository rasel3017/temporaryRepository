CREATE TABLE employee (
    emp_id INT PRIMARY KEY,
    first_name VARCHAR(30),
    last_name VARCHAR(30),
    salary DECIMAL(10,2),
    commission DECIMAL(10,2),
    hire_date DATE,
    dept_id INT,
    manager_id INT
);
INSERT INTO employee
(emp_id, first_name, last_name, salary, commission, hire_date, dept_id, manager_id)
VALUES
(101, 'Abu', 'Sayed', 35000, 2000, '2020-01-12', 10, 201),
(102, 'Maruf', 'Islam', 42000, NULL, '2021-03-15', 20, 202),
(103, 'Fahmin', 'Jafar', 28000, 1000, '2019-07-18', 10, 201),
(104, 'Rita', 'Akter', 50000, 3000, '2018-02-10', 30, 203),
(105, 'Rifat', 'Islam', 38000, NULL, '2022-04-05', 20, 202),
(106, 'Alif', 'Siam', 27000, 500, '2023-11-21', 40, 204);
CREATE TABLE department (
    dept_id INT PRIMARY KEY,
    department_name VARCHAR(30),
    location VARCHAR(30)
);
INSERT INTO department
(dept_id, department_name, location)
VALUES
(10, 'CSE', 'Dhaka'),
(20, 'EEE', 'Chittagong'),
(30, 'BBA', 'Khulna'),
(40, 'English', 'Rajshahi');
CREATE TABLE project (
    project_id VARCHAR(5) PRIMARY KEY,
    project_name VARCHAR(50),
    dept_id INT,
    budget DECIMAL(10,2)
);
INSERT INTO project
(project_id, project_name, dept_id, budget)
VALUES
('P1', 'AI Research', 10, 500000),
('P2', 'Smart Grid', 20, 700000),
('P3', 'Business ERP', 30, 350000),
('P4', 'Language Lab', 40, 200000);
SELECT UPPER(first_name) AS First_Name
FROM employee;
SELECT LEFT(first_name, 3) AS First_Three_Characters
FROM employee;
SELECT REPLACE(CONCAT(first_name, ' ', last_name), 'a', '*') AS Modified_Name
FROM employee;
