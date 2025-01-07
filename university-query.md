SELECT

1. Selezionare tutti gli studenti nati nel 1990 (160)
   1 : select \* from students where year(date_of_birth) = 1990;

2. Selezionare tutti i corsi che valgono più di 10 crediti (479)
   2 : select \* from courses where cfu > 10

3. Selezionare tutti gli studenti che hanno più di 30 anni
   3: select _ from students where year(date_of_birth) < 2025-30
   oppure quelli che hanno iniziato a 30 anni o più : select _ from students where year(date_of_birth) < enrolment_date - date_of_birth

4. Selezionare tutti i corsi del primo semestre del primo anno di un qualsiasi corso di
   laurea (286)
   4: select \* from courses where period = "I semestre" and year = 1

5. Selezionare tutti gli appelli d'esame che avvengono nel pomeriggio (dopo le 14) del
   20/06/2020 (21)
   5: SELECT \* FROM exams WHERE date = '2020-06-20' AND hour > '14:00:00';

6. Selezionare tutti i corsi di laurea magistrale (38)
   6: SELECT \*
   FROM degrees where level="magistrale"

7. Daquanti dipartimenti è composta l'università? (12)
   7: SELECT count(\*)
   FROM departments

8. Quanti sono gli insegnanti che non hanno un numero di telefono? (50)
   8: SELECT count(\*)
   FROM teachers where phone is null

9. Inserire nella tabella degli studenti un nuovo record con i propri dati (per il campo
   degree*id, inserire un valore casuale)
   9:
   INSERT INTO students (name, surname, date_of_birth, fiscal_code, enrolment_date, registration_number, email, degree_id)
   VALUES (
   'Mattia',
   'Placido',
   '2003-08-28',
   'PLCMTT03M28B354Z',
   '2024-09-12',
   '71117',
   'placido.mattia@gmail.com',
   FLOOR(RAND() * (SELECT COUNT(\_) FROM degrees)) + 1
   );

10. Cambiare il numero dell’ufficio del professor Pietro Rizzo in 126
    UPDATE teachers
    SET office_number = 126
    WHERE teacher_id = 58 ;

    oppure

    UPDATE teachers
    SET office_number = 126
    WHERE name = 'Pietro' AND surname = 'Rizzo';

    ma mi dice che non è sicuro updatare senza utilizzare la key, anche dopo aver disabilitato la safe mode

11. Eliminare dalla tabella studenti il record creato precedentemente al punto 9

    sapendo l'id : DELETE FROM students WHERE student_id = 5001;

    oppure DELETE FROM student WHERE name = "Mattia" AND surname = "Placido";

GROUPBY

1. Contare quanti iscritti ci sono stati ogni anno
   SELECT YEAR(enrolment_date), COUNT(\*)
   FROM students
   GROUP BY YEAR(enrolment_date);

2. Contare gli insegnanti che hanno l'ufficio nello stesso edificio

   SELECT office_address, COUNT(\*)
   FROM teachers
   GROUP BY office_address;

3. Calcolare la media dei voti di ogni appello d'esame

   SELECT exam_id, AVG(vote)
   FROM exam_student
   GROUP BY exam_id;

4. Contare quanti corsi di laurea ci sono per ogni dipartimento

//SBAGLIATO
SELECT departments.name, COUNT(\*)
FROM degrees
GROUP BY departments.name;
