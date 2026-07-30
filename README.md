SELECT *
FROM student
WHERE department = 'CSE'
   OR department = 'BBA';

   SELECT *
FROM student
WHERE department = 'CSE'
   OR department = 'EEE'
   AND points > 80;

   SELECT *
FROM student
WHERE (department = 'CSE'
    OR department = 'EEE')
  AND points > 80;
