# SQL Reeks 2

## JOINS

* Combineer rijen uit verschillende tabellen
* Rijen worden enkel gecombineerd als deze rijen voldoen aan een bepaalde booleaanse conditie (JOIN-conditie)
* Join-condities voldoen aan dezelfde regels als condities in de WHERE-
clausule en zijn dus booleaanse proposities.
* Join-condities kunnen dezelfde operatoren en functies bevatten als de
operatoren en functies die aangeleerd zijn in reeks 1.
* Er bestaan verschillende soorten joins: inner, left, right, full, cross...

### INNER JOIN

* Combineert rijen uit twee tabellen die voldoen aan de join-conditie
* Enkel rijen die in beide tabellen voorkomen worden geselecteerd

### LEFT JOIN

* Behoudt alle rijen uit de linker tabel en de rijen uit de rechter tabel die voldoen aan de join-conditie

### RIGHT JOIN

* Behoudt alle rijen uit de rechter tabel en de rijen uit de linker tabel die voldoen aan de join-conditie

### FULL JOIN

* Behoudt alle rijen uit beide tabellen, rijen die niet voldoen aan de join-conditie worden aangevuld met NULL-waarden

### JOIN-CONDITIE

* Join-condities worden toegevoegd aan de FROM-clausule
* ON kan vervangen worden door USING als de join-conditie gebaseerd is op een kolom met dezelfde naam in beide tabellen

### CROSS JOIN

* Combineert elke rij van de ene tabel met elke rij van de andere tabel

### MEERDERE JOINS

* Het is mogelijk om meerdere tabellen te joinen in één query