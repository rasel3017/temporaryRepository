SELECT CONCAT(first_name, ' ', last_name) AS Full_Name
FROM student;
SELECT CONCAT(first_name, ' ', last_name,
              ' got ', points,
              ' points, thank you') AS Message
FROM student
WHERE first_name = 'Osman';
