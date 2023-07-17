## DB university

- First query ```SELECT * FROM 'students' WHERE 'date_of_birth' LIKE '1990%';``` ,
- Second query ```SELECT * FROM `courses` WHERE `cfu` > 10; ```,
- Third query ```SELECT * FROM `students` WHERE TIMESTAMPDIFF(YEAR, `date_of_birth` , CURRENT_DATE )> 30; ```,
- Fourth query ```SELECT * FROM `courses` WHERE `period` LIKE 'I semestre' and `year` LIKE '1'; ```
- Fifth query ```SELECT * FROM `exams` WHERE `date` LIKE '2020-06-20' and TIME(`hour`) > '14:00:00'```
- Sixth query ```SELECT * FROM `degrees` WHERE `level` LIKE 'magistrale'```