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


# Ex - Query GROUP BY

1. Contare quanti iscritti ci sono stati ogni anno
    - ``` SELECT COUNT(*) as `number_of_students`, YEAR(`enrolment_date`) FROM `students` GROUP BY YEAR(`enrolment_date`); ```

2. Contare gli insegnanti che hanno l'ufficio nello stesso edificio
    - ```SELECT COUNT(*) as `number_of_teachers` , `office_address` FROM `teachers` GROUP BY `office_address`; ```

3. Calcolare la media dei voti di ogni appello d'esame
    -  ``` SELECT `exams`.`id` as `esame_id`, AVG(`exam_student`.`vote`) FROM `exams` JOIN `exam_student` on `exams`.`id` = `exam_student`.`exam_id` GROUP BY `exams`.`id`; ```

4. Contare quanti corsi di laurea ci sono per ogni dipartimento
    - SELECT `departments`.`name` as `dipartimento_nome`, COUNT(`degrees`.`id`) as `corsi` FROM `departments` JOIN `degrees` ON `departments`.`id` = `degrees`.`department_id` GROUP BY `departments`.`id`; 
