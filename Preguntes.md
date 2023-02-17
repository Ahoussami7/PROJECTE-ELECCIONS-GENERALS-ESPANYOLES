Apartat 2 (Preguntes)
=====================

Categoria 1: 5 preguntes de consultes simples: inclou una sola taula, funcions,
-------------------------------------------------------------------------------
funcions d'agregat o grups:
---------------------------
* * *
**Enumera els candidats (Ascendent) que siguin Titulars(T) i els que siguin Suplents(S),
la taula s'ha de veure de la següent manera:**

|candidat_id|T/S|


SELECT candidat_id, tipus AS "T/S"
    FROM candidats
    WHERE tipus = 'T' OR tipus = 'S'
    ORDER BY candidat_id;

* * * 
**Quina provincia te en el nom 2 vocals seguides.**

|provincia_id|nom|


SELECT provincia_id,nom
    FROM provincies
    WHERE nom RLIKE '[aeiou]{3}';

* * *
**Selecciona de les persones el seu total**

|Total|

SELECT COUNT(DISTINCT persona_id) AS Total
FROM persones;


* * *
**Quants municipis tenen un INE  99 de forma descendent:**

|municipi_id|nom|codi_ine|

SELECT municipi_id, nom, codi_ine
FROM municipis 
WHERE codi_ine LIKE '%99'
ORDER BY codi_ine DESC;

* * *
**De la taula candidatures selecciona les que tinguin un nom curt contenint la lletra 'A' i de candidatura_id només numeros parells.**

|candidatura_id|nomcurt|

SELECT candidatura_id, nom_curt AS nomcurt
FROM candidatures
WHERE MOD(candidatura_id,2) = 0 AND SUBSTRING(nom_curt, 5, 1) = 'A';

* * *
Categoria 2: 5 preguntes de consultes de combinacions de més d'una taula:
-------------------------------------------------------------------------
INNER JOINS, LEFT JOINS:
------------------------
* * *

**Quina es la hora d'apertura dels colegis electorals a la comunitat autonoma
de catalunya?**


|Com.Autonoma|horapt|

* * *
**Mostra la denominació de candidatura on hi hagin més vots en blanc.**


|Denm_Canddt|vtsblc|

* * *
**Quins candidats han sortit com a molt 10 vegades l'any 2016 on
el número de candidats obtenits per la candidatura siguin més de 2.**


|candidat|

* * *
**Mostra totes les sigles de candidatures que continguin totes les vocals en el seu nom i la suma dels vots provincials, municipals i de comunitats autonomes en una sola columna.**


|Sigles|Totalvots|

* * *
**Fes un top 5 candidatures amb menys de 100 vots provincials de l'any 2016, juntament amb el total de candidats de cada candidatura.**


|Candidatures|Totalcndts|

* * *
Categoria 4: 1 pregunta utilitzant WINDOW FUNCTIONS o recursivitat
------------------------------------------------------------------
* * *
Selecciona de cada empleat el total de vots(ca+mun+prov) de la seva candidatura.


|empleat|candidatura|Totalvots|


