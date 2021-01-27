# timetable
--Exo3
CREATE VIEW myview AS
SELECT DISTINCT C.codeCours, 
                T.jourCoursDate AS "Date",
                T. TRANCHE AS "Tranches",
                C.VOLUMEH AS "Horaires" 
FROM Cours C
JOIN Typehoraire T
ON C.codeCours= T.crsCodeCours
JOIN Jourcours J
ON J.dateJourCours=T.jourCoursDate
JOIN Coursdeclasse cls
ON T.crsCodeCours=cls.crsCodeCours
JOIN Classe Cl
ON cl.specialiteNomSpec=cls.classSpecialiteNomspec
WHERE T.jourCoursDate
IN ('lundi','mardi','mercredi','jeudi','vendredi','samedi') AND cls.classNiveauidNiveau=001;


--Exo4
alter table etudiant add password varchar(50);
update etudiant set password = ora_hash(matricule) where matricule = valeur;

-- Exo5
SET MARKUP HTML ON
SPOOL ON PREFORMAT OFF ENTMAP ON -
HEAD "<TITLE>Department Report</TITLE> -
<STYLE type='text/css'> -
<!-- BODY {background: #AACCC6} --> -
</STYLE>" –
 BODY "TEXT='#FF00Ff'" –
 TABLE "WIDTH='90%' BORDER='5'"
SPOOL SchoolTimeTABLE.html

SELECT DISTINCT C.codeCours,
                T.jourCoursDate AS "Date",
                C.VOLUMEH AS "Horaires"
FROM Cours C
JOIN Typehoraire T
ON C.codeCours= T.crsCodeCours
JOIN Jourcours J
ON J.dateJourCours=T.jourCoursDate
JOIN Coursdeclasse cls
ON T.crsCodeCours=cls.crsCodeCours
JOIN Classe Cl
ON cl.specialiteNomSpec=cls.classSpecialiteNomspec
JOIN Etudiantdeclasse et 
on cls.crsCodeCours=et.COURCODECOURS
JOIN ETUDIANT pp 
ON pp.MATRICULE=et.ETUDIANTMATRICULE
WHERE  et.ETUDIANTMATRICULE=&Matricule AND PASSWORD=&Password;
