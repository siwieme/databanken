# SQL Reeks 3

## WAT IS EEN SUBQUERY?

* Een subquery is een query die genest is in een andere query

## SUBQUERY IN FROM

* Een subquery in de FROM-clausule wordt uitgevoerd voor de hoofdquery
* De resultaten van de subquery worden gebruikt als invoer voor de hoofdquery
* Voorbeeld: `SELECT prof.werknemersid, prof.voornaam, prof.achternaam FROM ( SELECT * FROM werknemer WHERE functie = 'professor') AS prof`

## SUBQUERY IN WHERE

* Een subquery in de WHERE-clausule wordt uitgevoerd voor elke rij van de hoofdquery
* De resultaten van de subquery worden gebruikt als invoer voor de hoofdquery
* Voorbeeld: `SELECT * FROM werknemer WHERE werknemersid IN ( SELECT werknemersid FROM werknemer WHERE functie = 'professor')`

## SUBQUERY OPERATOREN: (NOT) IN

* `IN`: komt overeen met een waarde in de resultaten van de subquery
* `NOT IN`: komt niet overeen met een waarde in de resultaten van de subquery

## SUBQUERY OPERATOREN: (NOT) EXISTS

* `EXISTS`: retourneert `TRUE` als de subquery resultaten oplevert
* `NOT EXISTS`: retourneert `TRUE` als de subquery geen resultaten oplevert

## SUBQUERY OPERATOREN: ANY

* `ANY`: komt overeen met een waarde in de resultaten van de subquery

## SUBQUERY OPERATOREN: ALL

* `ALL`: komt overeen met alle waarden in de resultaten van de subquery

## SUBQUERY IN SELECT

* Een subquery in de SELECT-clausule retourneert één waarde
* Wordt meestal gebruikt wanneer je een aggregatiefunctie (bv. min, max, count, sum... zie reeks 4) wil uitvoeren, maar je deze aggregatiefunctie niet wil uitvoeren in de outside query
* Let op: de resultatentabel van de subquery mag, voor elke rij uit de outside query, uit slechts 1 rij bestaan