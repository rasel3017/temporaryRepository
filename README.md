SELECT *
FROM employee
WHERE first_name LIKE 'R%';
SELECT *
FROM employee
WHERE last_name LIKE '%n';
SELECT RPAD(first_name, 12, '*') AS Padded_Name
FROM employee;
