Apartat 2 (Preguntes)
=====================

Categoria 1: 5 preguntes de consultes simples: inclou una sola taula, funcions,
-------------------------------------------------------------------------------
funcions d'agregat o grups:
---------------------------
* * *
**Enumera els candidats (Ascendent) que siguin Titulars(T) i els que siguin Suplents(S),
la taula s'ha de veure de la següent manera:**


|Nom + cognoms|Titular|Suplent|

* * * 
**Segons la comunitat Catalunya, quin numero d'escons té ordenats descendent.**


|Candidatura|CAA|

* * *
**Enumerar els municipis amb el seu total de vots a candidatures i també
els vots nuts que hagin obtingut agrupat per vots a candidatures:**


|Municipis|Vtotals|VNuls|

* * *
**Quants municipis tenen Total municipal amb INE entre 100-101 Descendent:**


|Municipis|TMNCP|

* * *
**Els municipis que tinguin menys de 10000000 vots en blanc ha de tenir
les dades oficials amb valor No.**

|Municipis|Vots blanc|NoOficial|

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
**Fes un top 5 candidatures amb menys vots de l'any 2016, juntament amb el total de candidats de cada candidatura.**


|Candidatures|Totalcndts|

* * *
Categoria 4: 1 pregunta utilitzant WINDOW FUNCTIONS o recursivitat
------------------------------------------------------------------
* * *
Selecciona de cada empleat el total de vots(ca+mun+prov) de la seva candidatura.


|empleat|candidatura|Totalvots|


