1. Selezionare tutti gli studenti nati nel 1990 (160)
SELECT * FROM `students` WHERE YEAR(`date_of_birth`) = 1990

2. Selezionare tutti i corsi che valgono più di 10 crediti (479)
SELECT * FROM `courses` WHERE `cfu` > 10


3. Selezionare tutti gli studenti che hanno più di 30 anni
SELECT * FROM `students` WHERE YEAR(CURRENT_DATE) -YEAR(`date_of_birth`) > 30;

4. Selezionare tutti i corsi del primo semestre del primo anno di un qualsiasi corso di
laurea (286)
SELECT * FROM `courses` WHERE `period` = "I semestre" AND `year` = 1

5. Selezionare tutti gli appelli d'esame che avvengono nel pomeriggio (dopo le 14) del
20/06/2020 (21)
SELECT * FROM `exams` WHERE `date` LIKE "2020-06-20" AND HOUR(`hour`) > 14;

6. Selezionare tutti i corsi di laurea magistrale (38)
SELECT * FROM `degrees` WHERE `level` LIKE "magistrale"


7. Da quanti dipartimenti è composta l'università? (12)
SELECT COUNT(*) FROM `departments`

8. Quanti sono gli insegnanti che non hanno un numero di telefono? (50)
SELECT * FROM `teachers` WHERE `phone` IS NULL




#EX - Query con GROUP BY

1. Contare quanti iscritti ci sono stati ogni anno
SELECT COUNT(`id`) AS `studenti_iscritti`, YEAR(`enrolment_date`) AS `anno`
FROM `students`
GROUP BY YEAR(`enrolment_date`)

2. Contare gli insegnanti che hanno l'ufficio nello stesso edificio
SELECT COUNT(`id`) AS `insegnanti`, `office_address` as `ufficio` 
FROM `teachers`
GROUP BY (`office_address`)
ORDER BY (`insegnanti`) DESC

3. Calcolare la media dei voti di ogni appello d'esame
SELECT AVG(`vote`)
FROM `exam_student`

4. Contare quanti corsi di laurea ci sono per ogni dipartimento
SELECT COUNT(`id`) AS `numero_corsi`, `department_id` as `dipartimento`
FROM `degrees` 
GROUP BY (`department_id`)

#EX - Query con JOIN

1. Selezionare tutti gli studenti iscritti al Corso di Laurea in Economia
SELECT `degrees`.`name` AS `nome_corso`, `students`.`name`, `students`.`surname`
FROM `degrees`
INNER JOIN `students`
ON `degrees`.`id` = `students`.`degree_id`
WHERE `degrees`.`name` = "Corso di Laurea in Economia"

2. Selezionare tutti i Corsi di Laurea Magistrale del Dipartimento di Neuroscienze
SELECT * 
FROM `departments` 
INNER JOIN `degrees`
ON `departments`.`id` = `degrees`.`department_id`
WHERE `departments`.`id` = 7 AND `degrees`.`level` = "magistrale"

3. Selezionare tutti i corsi in cui insegna Fulvio Amato (id=44)
SELECT * 
FROM `courses` 
INNER JOIN `course_teacher`
ON `courses`.`id` = `course_teacher`.`teacher_id`
WHERE `course_teacher`.`teacher_id` = 47

4. Selezionare tutti gli studenti con i dati relativi al corso di laurea a cui sono iscritti e il relativo dipartimento, in ordine alfabetico per cognome e nome

SELECT `students`.`surname`, `students`.`name`, `degrees`.`name`, `departments`.`name`
FROM `students`
INNER JOIN `degrees` 
ON `degrees`.`id` = `students`.`degree_id`
INNER JOIN `departments` 
ON `departments`.`id` = `degrees`.`department_id`
ORDER BY `students`.`surname`, `students`.`name`

5. Selezionare tutti i corsi di laurea con i relativi corsi e insegnanti

SELECT `degrees`.`name`, `courses`.`name`, `teachers`.`name`, `teachers`.`surname`
FROM `degrees`
INNER JOIN `courses` 
ON `degrees`.`id` = `courses`.`degree_id`
INNER JOIN `course_teacher` 
ON `courses`.`id` = `course_teacher`.`course_id`
INNER JOIN `teachers` 
ON `teachers`.`id` = `course_teacher`.`teacher_id`;


6. Selezionare tutti i docenti che insegnano nel Dipartimento di Matematica (54)


7. BONUS: Selezionare per ogni studente il numero di tentativi sostenuti per ogni esame, stampando anche il voto massimo. Successivamente, filtrare i tentativi con voto minimo 18.

#BONUS - Query con JOIN

1. Selezionare tutti i corsi del Corso di Laurea in Informatica (22)
2. Selezionare le informazioni sul corso con id = 144, con tutti i relativi appelli d’esame
3. Selezionare a quale dipartimento appartiene il Corso di Laurea in Diritto dell'Economia (Dipartimento di Scienze politiche, giuridiche e studi internazionali)
4. Selezionare tutti gli appelli d'esame del Corso di Laurea Magistrale in Fisica del primo anno
5. Selezionare tutti i docenti che insegnano nel Corso di Laurea in Lettere (21)
6. Selezionare il libretto universitario di Mirco Messina (matricola n. 620320)
7. Selezionare il voto medio di superamento d'esame per ogni corso, con anche i dati del corso di laurea associato, ordinati per media voto decrescente
