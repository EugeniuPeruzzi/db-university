## DB university

- First query ```SELECT * FROM 'students' WHERE 'date_of_birth' LIKE '1990%';``` ,
- Second query ```SELECT * FROM `courses` WHERE `cfu` > 10; ```,
- Third query ```SELECT * FROM `students` WHERE TIMESTAMPDIFF(YEAR, `date_of_birth` , CURRENT_DATE )> 30; ```,
