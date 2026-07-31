SELECT CURDATE() AS Today_Date;
SELECT CONCAT(first_name, ' ', last_name) AS Employee_Name,
       TIMESTAMPDIFF(MONTH, hire_date, CURDATE()) AS Months_Worked
FROM employee;
SELECT CONCAT(first_name, ' ', last_name) AS Employee_Name,
       hire_date,
       DATE_ADD(hire_date,
                INTERVAL ((6 - DAYOFWEEK(hire_date) + 7) % 7) + 1 DAY) AS Next_Friday
FROM employee;
SELECT CONCAT(first_name, ' ', last_name) AS Employee_Name,
       LAST_DAY(hire_date) AS Last_Day
FROM employee;
SELECT CONCAT(first_name, ' ', last_name) AS Employee_Name,
       DATE_ADD(hire_date, INTERVAL 6 MONTH) AS New_Hire_Date
FROM employee;
SELECT *
FROM employee
WHERE hire_date >= DATE_SUB(CURDATE(), INTERVAL 5 YEAR);
