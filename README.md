# timetable
--Exo3
CREATE VIEW emploisdetemps AS 
SELECT DISTINCT C.codeCours,
                T.jourCoursDate  
FROM Cours C
JOIN Typehoraire T
ON C.codeCours= T.crsCodeCours
JOIN Jourcours J
ON J.dateJourCours=T.jourCoursDate
JOIN Coursdeclasse cls
ON  T.crsCodeCours=cls.crsCodeCours
JOIN Classe Cl
ON cl.specialiteNomSpec=cls.classSpecialiteNomspec
WHERE T.jourCoursDate 
IN ('lundi','mardi','mercredi','jeudi','vendredi','samedi');


--Exo4
alter table etudiant add password varchar(50);
update etudiant set password = ora_hash(matricule) where matricule = valeur;


CREATE VIEW emploisdetemps AS 
SELECT DISTINCT C.codeCours, T.jourCoursDate  FROM Cours C
JOIN Typehoraire T
ON C.codeCours= T.crsCodeCours
JOIN Jourcours J
ON J.dateJourCours=T.jourCoursDate
JOIN Coursdeclasse cls
ON  T.crsCodeCours=cls.crsCodeCours
JOIN Classe Cl
ON cl.specialiteNomSpec=cls.classSpecialiteNomspec
WHERE T.jourCoursDate 
IN ('lundi','mardi','mercredi','jeudi','vendredi','samedi');




-- Exo5
SET ECHO OFF
SET MARKUP HTML ON SPOOL ON

SPOOL timetable.HTML
SELECT DISTINCT T.jourCoursDate as jours ,
                  C.intituleCourt ||'('||C.codeCours||')' as "Nom du cours" ,
                    C.credits as "Credits",
                    'Trim '|| C.periodeAcademiqueIdTrim  as "Trimestre du cours",
                    ce.specialiteNomSpec || cd.classNiveauidNiveau as "Specialite",
                    T.tranche ||'heures' as "Horaires"
FROM Cours C
JOIN Typehoraire T
ON C.codeCours= T.crsCodeCours
JOIN Jourcours j
ON J.dateJourCours=T.jourCoursDate
JOIN Coursdeclasse cd
ON  T.crsCodeCours=cd.crsCodeCours
JOIN Classe ce
ON ce.specialiteNomSpec=cd.classSpecialiteNomspec
INNER JOIN ClassePeriodeacademique ca
ON C.periodeAcademiqueIdTrim=ca.PERIODEACADEMIQUEIDTRIM
WHERE ce.specialiteNomSpec='TIPAM'
AND cd.classNiveauidNiveau=002;
AND   etudiantMatricule = &matricule;
ORDER BY T.jourCoursDate ASC; 
SPOOL OFF
SET MARKUP HTML OFF
SET ECHO ON


