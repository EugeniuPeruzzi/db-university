## DB university

- First query : Selezionare tutti gli studenti nati nel 1990 (160)
    - ```SELECT * FROM 'students' WHERE 'date_of_birth' LIKE '1990%';``` ,
- Second query : Selezionare tutti i corsi che valgono piu di 10 crditi (479)
    - ```SELECT * FROM `courses` WHERE `cfu` > 10; ```,
- Third query : Selezionare tutti gli studenti che hanno piu di 30 anni
    - ```SELECT * FROM `students` WHERE TIMESTAMPDIFF(YEAR, `date_of_birth` , CURRENT_DATE )> 30; ```,
- Fourth query : Selezionare tutti i corsi del primo semestre del primo anno di un qualsiasi corso di laurea 
    - ```SELECT * FROM `courses` WHERE `period` LIKE 'I semestre' and `year` LIKE '1'; ```
- Fifth query : Selezionare tutti gli apelli d'esame che vengono nel pomeriggio dopo le 14.00 in data di 20/06/2020
    - ```SELECT * FROM `exams` WHERE `date` LIKE '2020-06-20' and TIME(`hour`) > '14:00:00'```
- Sixth query : Seleziona tutti i corsi di laurea magistrale 
    - ```SELECT * FROM `degrees` WHERE `level` LIKE 'magistrale'```
- Seventh query : Da quanti dipartimenti e composta l'universita
    - ```SELECT COUNT(`name`) as 'departmets_count' FROM `departments`;``` || ```SELECT COUNT(`name`) FROM `departments`;``` (you get table named COUNT)
- Eight query : Quanti sono gli insegnanti che non hanno un numero di telefono?
    - ```SELECT * FROM `teachers` WHERE `phone` IS NULL```