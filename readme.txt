GROUP BY

1. Contare quanti iscritti ci sono stati ogni anno

SELECT `year`, COUNT(*) AS numero_iscritti
FROM `courses`
GROUP BY `year`;


2. Contare gli insegnanti che hanno l'ufficio nello stesso edificio

SELECT office_address, COUNT(*) as insegnanti 
FROM `teachers`
GROUP BY office_address;


3. Calcolare la media dei voti di ogni appello d'esame

SELECT `exam_id`AS Esame, AVG(`vote`) AS Media_voti
FROM `exam_student`
GROUP BY `exam_id`;


4. Contare quanti corsi di laurea ci sono per ogni dipartimento

SELECT`department_id` AS Dipartimento, COUNT(*) AS Numero_di_Corsi
FROM `degrees`
GROUP BY `department_id`;


JOIN

1. Selezionare tutti gli studenti iscritti al Corso di Laurea in Economia

SELECT students.name, students.surname
FROM students
JOIN degrees ON students.degree_id = degrees.id
WHERE degrees.name = 'Corso di Laurea in Economia';

2. Selezionare tutti i Corsi di Laurea Magistrale del 

SELECT degrees.*
FROM degrees
JOIN departments ON degrees.department_id = departments.id
WHERE departments.name = 'Dipartimento di Neuroscienze' AND degrees.level = 'Magistrale';


3. Selezionare tutti i corsi in cui insegna Fulvio Amato (id=44)

SELECT courses.*
FROM courses
JOIN course_teacher ON courses.id = course_teacher.course_id
JOIN teachers ON course_teacher.teacher_id = teachers.id
WHERE teachers.id = 44;

4. Selezionare tutti gli studenti con i dati relativi al corso di laurea a cui sono iscritti e il
relativo dipartimento, in ordine alfabetico per cognome e nome

SELECT students.*, degrees.name, departments.name
FROM students
JOIN degrees ON students.degree_id = degrees.id
JOIN departments ON degrees.department_id = departments.id
ORDER BY students.surname, students.name;

5. Selezionare tutti i corsi di laurea con i relativi corsi e insegnanti

SELECT degrees.*, courses.*, teachers.*
FROM degrees
JOIN courses ON degrees.id = courses.degree_id
JOIN course_teacher ON courses.id = course_teacher.course_id
JOIN teachers ON course_teacher.teacher_id = teachers.id;

6. Selezionare tutti i docenti che insegnano nel Dipartimento di Matematica (54)

SELECT teachers.*
FROM teachers
JOIN course_teacher ON teachers.id = course_teacher.teacher_id
JOIN courses ON courses.id = course_teacher.course_id
JOIN degrees ON courses.degree_id = degrees.id
JOIN departments ON departments.id = degrees.department_id
WHERE departments.name = 'Dipartimento di Matematica';

7. BONUS: Selezionare per ogni studente quanti tentativi d’esame ha sostenuto per
superare ciascuno dei suoi esami