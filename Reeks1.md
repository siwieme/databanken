# SQL Reeks 1

## SELECT & FROM

* SELECT-clausule
    * Selecteer kolommen van een tabel
    * Laat aliasing toe: `SELECT kolom AS alias`
    * Introduceer nieuwe kolommen door toepassing van functies en operatoren (extend): `SELECT kolom1 + kolom2 AS kolom3`
* FROM-clausule:
    * Bepaal de tabellen waarmee gewerkt wordt, dit is mogelijks:
        * Een enkele tabel
        * Een join van meerdere tabellen (reeks2)
        * Een zelf-gedefinieerde tabel (reeks3)
* Know-how
    * Selecteer ALLE kolommen van een tabel: `SELECT * FROM tabel`
    * Selecteer SOMMIGE kolommen van een tabel: `SELECT kolom1, kolom2 FROM tabel`
    * Aliasing van kolommen: `SELECT kolom1 AS alias1, kolom2 AS alias2 FROM tabel` OF `SELECT kolom1 alias1, kolom2 alias2 FROM tabel`
    * Concatenatie van kolommen: `SELECT kolom1 || ' - ' || kolom2 AS kolom3 FROM tabel`
    * Unieke rijen: `SELECT DISTINCT kolom1 FROM tabel`
    * Conditionele selectie (CASE): `SELECT CASE WHEN kolom1 > 10 THEN 'Ja' ELSE 'Nee' END AS kolom2 FROM tabel`

## WHERE

* Selecteer rijen in de tabel die voldoen aan een bepaalde voorwaarde
* Enkel rijen die voldoen aan de voorwaarde worden geselecteerd
* Operatoren: AND, OR, NOT
* Evaluatievolgorde: NOT > AND > OR, maar door gebruik van ( ) kan de volgorde aangepast worden

## OPERATOREN EN FUNCTIES

* Vergelijkingsoperatoren:
    * <, >, =, <=, >=, <> (niet gelijk aan)
    * (NOT) BETWEEN x AND y
    * IS (NOT) NULL
    * (NOT) LIKE 'patroon' (met % en _ als wildcards)
    * (NOT) ILIKE 'patroon' (case-insensitive)
    * % is 0 of meer karakters, _ is 1 karakter
* Wiskundige operatoren:
    * +, -, *, /, % (modulo)
    * |/ (wortel), ^ (macht)
* Stringfuncties:
    * concat(kolom1, kolom2, ...)
    * lower(kolom), upper(kolom)
    * substr(kolom, start, lengte)
    * length(kolom)
    * position('substring' IN kolom)
    * replace(kolom, 'oud', 'nieuw')
    * reverse(kolom)
* Wiskundige functies
    * abs(kolom)
    * floor(kolom), ceil(kolom): rond af naar beneden/boven tot geheel getal
    * round(kolom, aantal_decimalen): rond af naar aantal_decimalen met -1 = tiental, -2 = honderdtal, ...
    * trunc(kolom, aantal_decimalen): kap af naar aantal_decimalen met -1 = tiental, -2 = honderdtal, ...
* Array functies:
    * unnest(array): maak van een array een collectie rijen
    * array_length(array, dimensie): geef lengte van array of dimensie
    * string_to_array(string, separator): maak van een string een array
* Casting:
    * cast(kolom AS type): cast naar type

## ORDER BY

* Sorteer de resultaten van een query
* NULLS FIRST/LAST: bepaal of NULL-waarden eerst of laat gesorteerd worden

## EVALUATIEVOLGORDE

1. QUERY
2. FROM
3. WHERE
4. SELECT
5. ORDER BY
6. RESULTAAT

* Betekenis: als je een kolom hernoemt in de SELECT-clausule, kan je niet aan de hand van zijn alias naar deze kolom refereren in de WHERE-clausule, aangezien de WHERE- clausule intern door PostgreSQL voor de SELECT-clausule wordt geëvalueerd