## DB university

- First query : Selezionare tutti gli studenti nati nel 1990 (160)
    ```
    SELECT * FROM 'students' WHERE 'date_of_birth' LIKE '1990%';
    ``` 
- Second query : Selezionare tutti i corsi che valgono piu di 10 crditi (479)
    ```
    SELECT * FROM `courses` WHERE `cfu` > 10;
    ```,
- Third query : Selezionare tutti gli studenti che hanno piu di 30 anni
    ```
    SELECT * FROM `students` WHERE TIMESTAMPDIFF(YEAR, `date_of_birth` , CURRENT_DATE )> 30; 
    ```,
- Fourth query : Selezionare tutti i corsi del primo semestre del primo anno di un qualsiasi corso di laurea 
    ```
    SELECT * FROM `courses` WHERE `period` LIKE 'I semestre' and `year` LIKE '1'; 
    ```
- Fifth query : Selezionare tutti gli apelli d'esame che vengono nel pomeriggio dopo le 14.00 in data di 20/06/2020
    ```
    SELECT * FROM `exams` WHERE `date` LIKE '2020-06-20' and TIME(`hour`) > '14:00:00'
    ```
- Sixth query : Seleziona tutti i corsi di laurea magistrale 
    ```
    SELECT * FROM `degrees` WHERE `level` LIKE 'magistrale'
    ```
- Seventh query : Da quanti dipartimenti e composta l'universita
    ```
    SELECT COUNT(`name`) as 'departmets_count' FROM `departments`;

    || 

    SELECT COUNT(`name`) FROM `departments`; (you get table named COUNT)
    ``` 
- Eight query : Quanti sono gli insegnanti che non hanno un numero di telefono?
    ```
    SELECT * FROM `teachers` WHERE `phone` IS NULL
    ```


### Ex - Query GROUP BY

1. Contare quanti iscritti ci sono stati ogni anno
    ``` 
    SELECT COUNT(*) as `number_of_students`, YEAR(`enrolment_date`) FROM `students` GROUP BY YEAR(`enrolment_date`); 
    ```

2. Contare gli insegnanti che hanno l'ufficio nello stesso edificio
    ```
    SELECT COUNT(*) as `number_of_teachers` , `office_address` FROM `teachers` GROUP BY `office_address`; 
    ```

3. Calcolare la media dei voti di ogni appello d'esame
    ``` 
    SELECT `exams`.`id` as `esame_id`, AVG(`exam_student`.`vote`) FROM `exams` JOIN `exam_student` on `exams`.`id` = `exam_student`.`exam_id` GROUP BY `exams`.`id`; 
    ```

4. Contare quanti corsi di laurea ci sono per ogni dipartimento
    ```
    SELECT `departments`.`name` as `dipartimento_nome`, COUNT(`degrees`.`id`) as `corsi` FROM `departments` JOIN `degrees` ON `departments`.`id` = `degrees`.`department_id` GROUP BY `departments`.`id`; 
    ```


### Ex - Query JOIN 

1. Selezionare tutti gli studenti iscritti al Corso di Laurea in Economia 
    ``` 
    SELECT   COUNT(`students`.`id`) AS `numero_studenti` ,`degrees`.`name` as `corso_di_laurea` FROM `degrees` JOIN `students` ON `degrees`.`id` = `students`.`degree_id` WHERE `degrees`.`name` LIKE 'Corso di Laurea in Economia'; 
    ```

2. Selezionare tutti i Corsi di Laurea Magistrale del Dipartimento di Neuroscienze
    ``` 
    SELECT `departments`.`name` AS `dipartimento`, `degrees`.`name` AS `corso_laurea` FROM `departments`  JOIN `degrees` ON `departments`.`id` = `degrees`.`department_id`  WHERE `degrees`.`level` LIKE 'magistrale' AND `departments`.`name` LIKE 'Dipartimento di Neuroscienze'
    ```

3. Selezionare tutti i corsi in cui insegna Fulvio Amato (id=44)
    ``` 
    SELECT `courses`.`name` as `nome_corso`, `teachers`.* FROM `courses` JOIN `course_teacher` on `courses`.`id` = `course_teacher`.`course_id` JOIN `teachers` on `course_teacher`.`teacher_id` = `teachers`.`id` WHERE `teacher_id` = 44 
    ```

4. Selezionare tutti gli studenti con i dati relativi al corso di laurea a cui sono iscritti e il relativo dipartimento, in ordine alfabetico per cognome e nome
    ```
    SELECT `students`.* , `degrees`.`name` as `cors_laurea`, `departments`.`name`  FROM `students` JOIN `degrees` ON `students`.`degree_id` = `degrees`.`id` JOIN `departments` ON `degrees`.`department_id` = `departments`.`id` ORDER BY `students`.`name`, `students`.`surname` 
    ```

5. Selezionare tutti i corsi di laurea con i relativi corsi e insegnanti
    ```
    SELECT `degrees`.* , `courses`.`name` as `nome_corso`, `teachers`.`name` as `nome_prof`, `teachers`.`surname` as `cognome_prof` FROM `degrees` JOIN `courses` ON `degrees`.`id` = `courses`.`degree_id` JOIN `course_teacher` ON `courses`.`id` = `course_teacher`.`course_id` JOIN `teachers` ON `course_teacher`.`teacher_id` = `teachers`.`id` JOIN `departments` ON `degrees`.`department_id` = `departments`.`id`; 
    ```

6. Selezionare tutti i docenti che insegnano nel Dipartimento di Matematica (54)
    ```
    SELECT DISTINCT `teachers`.`name` as `nome_prof`, `teachers`.`surname` as `cognome_prof`, `departments`.`name` as `nome_dipartimento` FROM `teachers` JOIN `course_teacher` ON `teachers`.`id` = `course_teacher`.`teacher_id` JOIN `courses` ON `course_teacher`.`course_id` = `courses`.`id` JOIN `degrees` ON `courses`.`degree_id` = `degrees`.`id` JOIN `departments` ON `degrees`.`department_id` = `departments`.`id` WHERE `departments`.`name` LIKE 'Dipartimento di Matematica'; 
    ```

7. BONUS: Selezionare per ogni studente il numero di tentativi sostenuti per ogni esame, stampando anche il voto massimo. Successivamente,filtrare i tentativi con voto minimo 18
    ```
    SELECT `students`.*, COUNT(`exam_student`.`student_id`) as `conteggio_studenti`, MAX(`exam_student`.`vote`) as `voto_massimo` FROM `students` JOIN `exam_student` ON `students`.`id` = `exam_student`.`student_id` JOIN `exams` ON `exam_student`.`exam_id` = `exams`.`id` GROUP BY `students`.`id` HAVING MIN(`exam_student`.`vote`) < 18; 
    ```
