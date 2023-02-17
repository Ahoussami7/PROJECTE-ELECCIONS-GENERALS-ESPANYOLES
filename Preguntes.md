Apartat 2 (Preguntes)
=====================

### Preguntes Simples
    
**Enumera els candidats (Ascendent) que siguin Titulars(T) i els que siguin Suplents(S), la taula s'ha de veure de la següent manera:** 

SELECT candidat_id, tipus AS 'T/S'
FROM candidats
ORDER BY candidat_id;

* * *
**Segons la comunitat Catalunya, quin numero d'escons té ordenats descendent.**

SELECT nom, num_escons
FROM provincies
ORDER BY num_escons DESC;

* * *
**Quants municipis tenen un INE  99 de forma descendent:**

SELECT municipi_id, nom, codi_ine
FROM municipis 
WHERE codi_ine LIKE '%99'
ORDER BY codi_ine DESC;

* * *
**De la taula candidatures selecciona les que tinguin un nom curt entre 1 i 4 lletres i de candidatura_id només numeros parells.**

SELECT candidatura_id, nom_curt AS nomcurt
FROM candidatures
WHERE MOD(candidatura_id,2) = 0 AND SUBSTRING(nom_curt, 5, 1) = 'A';

* * *
**Selecciona els 10 primers municipis i transforma els caràcters especials a normals, ordenat pel nom ascendent.**

SELECT COUNT(DISTINCT persona_id) AS Total
FROM persones;

* * *
-- INNER JOINS

* * *
**Fes un top 5 candidatures amb menys vots provincials de l'any 2016, juntament amb el total de candidats de cada candidatura.**

SELECT cds.candidatura_id AS Candidatures, vcp.vots
FROM candidatures cds
INNER JOIN vots_candidatures_prov vcp ON cds.candidatura_id = vcp.candidatura_id
INNER JOIN candidats can ON cds.candidatura_id = can.candidatura_id
WHERE vots < 100;

* * *
**Selecciona els noms dels municipis, i també el nom de la provincia que pertanyen.**

SELECT mnc.nom AS nomMNC, provincies.nom AS nomPRV
FROM municipis mnc
LEFT JOIN provincies ON mnc.provincia_id = provincies.provincia_id;

* * *
**Selecciona de les comunitats autonomes i junta-hi la columna nom de provincies i també el codi_ine d'aquestes dues taules.**

|nomca|nomprov|ine_ca_prov|

SELECT ca.nom AS nomca, prov.nom,CONCAT(ca.codi_ine,'_',prov.codi_ine) AS ine_ca_prov
FROM comunitats_autonomes ca
CROSS JOIN provincies prov;

* * *
**Selecciona les provincies juntament amb el seu numero d'escons i el seu total de vots.**

|provincia_id|nom|num_escons|Totalvots|

SELECT p.provincia_id,p.nom,p.num_escons,SUM(vp.vots) AS 'Totalvots'
FROM provincies p
INNER JOIN vots_candidatures_prov vp ON p.provincia_id = vp.provincia_id
GROUP BY provincia_id;

* * *
**Selecciona el municipi i el seu nom, també junta-hi les mateixes columnes per comunitats autonomes.**

SELECT DISTINCT m.municipi_id, m.nom, ca.comunitat_aut_id, ca.nom
From municipis m
INNER JOIN provincies p ON p.provincia_id = m.provincia_id
INNER JOIN comunitats_autonomes ca ON ca.comunitat_aut_id = p.comunitat_aut_id
WHERE ca.nom = 'ANDALUCIA';

* * *
### Subconsultes

* * *
**Selecciona els candidats que tinguin de nom Robert.**

SELECT candidat_id, num_ordre
FROM candidats
WHERE persona_id IN (
SELECT persona_id
FROM persones
WHERE upper(nom)="Robert" );

* * * 
**Selecciona les provincies de les comunitats autonomes catalanes.**
SELECT provincia_id, nom
FROM provincies
WHERE comunitat_aut_id IN (
	SELECT comunitat_aut_id
	FROM comunitats_autonomes
	WHERE UPPER(nom) IN ("CATALUNYA", "COMUNITAT VALENCIANA", "ILLES BALEARS"));
    
* * *
**Obté totes les candidatures que han tingut un major número de vots que la mitjana dels vots provincials.**

SELECT nom_curt, prov.vots
FROM candidatures ca
INNER JOIN vots_candidatures_prov prov ON ca.candidatura_id = prov.candidatura_id
WHERE ca.candidatura_id IN (
    SELECT candidatura_id
    FROM vots_candidatures_prov
    WHERE prov.vots > (
        SELECT AVG(vots)
        FROM vots_candidatures_prov
    )
);

* * *
**Per cada partit digues el número de candidats que té.**

SELECT nom_curt, nom_llarg, (SELECT COUNT(*) FROM candidats WHERE candidatura_id = ca.candidatura_id) AS num_candidats
FROM candidatures ca;

* * *
**Selecciona per la candidatura VOX els vots de tots els partits.**

SELECT nom_curt, 
  (SELECT SUM(vots) FROM vots_candidatures_prov WHERE candidatura_id = ca.candidatura_id) AS total_votos
FROM candidatures ca
WHERE codi_candidatura = (SELECT codi_candidatura FROM candidatures WHERE UPPER(nom_curt) = 'VOX');

* * *
-- Window Function

**Per cada municipi digues quants districtes té.**

SELECT municipi_id, nom, codi_ine, provincia_id, MAX(districte)
	OVER (PARTITION BY provincia_id) AS districtes
	FROM municipis;
    

