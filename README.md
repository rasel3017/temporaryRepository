SELECT *
FROM student
WHERE points <> 5;
SELECT *
FROM product
WHERE price BETWEEN 2000 AND 15000;
SELECT *
FROM student
WHERE first_name LIKE '%hi%';
SELECT *
FROM student
WHERE first_name LIKE '%r';
SELECT *
FROM product
WHERE quantity IS NULL;
