## DB university

- First query : Selezionare tutti gli studenti nati nel 1990 (160)
    - ```SELECT * FROM 'students' WHERE 'date_of_birth' LIKE '1990%';``` ,
- Second query : SDelezionare tutti i corsi che valgono piu di 10 crditi (479)
    - ```SELECT * FROM `courses` WHERE `cfu` > 10; ```,
- Third query ```SELECT * FROM `students` WHERE TIMESTAMPDIFF(YEAR, `date_of_birth` , CURRENT_DATE )> 30; ```,
- Fourth query ```SELECT * FROM `courses` WHERE `period` LIKE 'I semestre' and `year` LIKE '1'; ```
- Fifth query ```SELECT * FROM `exams` WHERE `date` LIKE '2020-06-20' and TIME(`hour`) > '14:00:00'```
- Sixth query ```SELECT * FROM `degrees` WHERE `level` LIKE 'magistrale'```
- Seventh query ```SELECT COUNT(`name`) as 'departmets_count' FROM `departments`;``` || ```SELECT COUNT(`name`) FROM `departments`;``` (to get table named COUNT)
- Eight query ```SELECT * FROM `teachers` WHERE `phone` IS NULL```