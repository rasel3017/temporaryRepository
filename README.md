SELECT salary,
       ROUND(salary / 3, 2) AS Divided_Salary
FROM employee;
SELECT salary,
       MOD(salary, 5000) AS Remainder
FROM employee;
SELECT salary,
       ABS(salary - 40000) AS Absolute_Difference
FROM employee;
SELECT salary,
       POWER(salary, 2) AS Salary_Square
FROM employee;
