SELECT CONCAT(first_name, ' ', last_name) AS Employee_Name,
       DATE_FORMAT(hire_date, '%W, %d %M %Y') AS Formatted_Date
FROM employee;

SELECT CONCAT('$', FORMAT(salary, 2)) AS Formatted_Salary
FROM employee;

SELECT STR_TO_DATE('25 December 2024', '%d %M %Y') AS Converted_Date;

SELECT DATE_FORMAT(CURDATE(), '%W, %d %M %Y') AS Today_Date;

SELECT salary,
       commission,
       NULLIF(salary, commission) AS Result
FROM employee;

SELECT first_name,
       COALESCE(commission, salary) AS Commission_Or_Salary
FROM employee;

SELECT first_name,
       salary + IFNULL(commission, 0) AS Total_Income
FROM employee;

SELECT first_name,
       salary,
       CASE
           WHEN salary >= 50000 THEN 'High'
           WHEN salary >= 35000 THEN 'Medium'
           ELSE 'Low'
       END AS Salary_Grade
FROM employee;

SELECT first_name,
       hire_date,
       CASE
           WHEN TIMESTAMPDIFF(YEAR, hire_date, CURDATE()) > 5 THEN 'Senior'
           ELSE 'Junior'
       END AS Experience_Level
FROM employee;

SELECT dept_id,
       CASE dept_id
           WHEN 10 THEN 'CSE'
           WHEN 20 THEN 'EEE'
           WHEN 30 THEN 'BBA'
           WHEN 40 THEN 'English'
       END AS Department_Name
FROM employee;

SELECT MAX(salary) AS Maximum_Salary
FROM employee;

SELECT SUM(salary) AS Total_Salary
FROM employee;

SELECT COUNT(*) AS Total_Employees
FROM employee;
SELECT COUNT(commission) AS Employees_With_Commission
FROM employee;

SELECT dept_id,
       MAX(salary) AS Highest_Salary
FROM employee
GROUP BY dept_id;

SELECT dept_id,
       COUNT(*) AS Total_Employees
FROM employee
GROUP BY dept_id
HAVING COUNT(*) > 1;

SELECT dept_id,
       AVG(salary) AS Average_Salary
FROM employee
GROUP BY dept_id
HAVING AVG(salary) > 35000;

SELECT d.dept_id,
       d.department_name,
       e.first_name,
       e.last_name
FROM department d
LEFT JOIN employee e
ON d.dept_id = e.dept_id;
SELECT e.first_name,
       e.last_name,
       d.department_name,
       d.location
FROM employee e
JOIN department d
ON e.dept_id = d.dept_id
WHERE d.location = 'Dhaka';

SELECT d.dept_id,
       d.department_name
FROM department d
LEFT JOIN employee e
ON d.dept_id = e.dept_id
WHERE e.emp_id IS NULL;

SELECT first_name,
       last_name,
       salary,
       dept_id
FROM employee e
WHERE salary >
(
    SELECT AVG(salary)
    FROM employee
    WHERE dept_id = e.dept_id
);

SELECT CONCAT(first_name, ' ', last_name) AS Employee_Name,
       manager_id
FROM employee;
