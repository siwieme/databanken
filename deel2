1. Vind de jongste en oudste wielrenners per land.

Gebruik een window-functie om wielrenners te rangschikken op geboortedatum binnen hun land.
```sql
WITH Ranking AS (
    SELECT 
        wielrennerid, naam, land, geboortedatum,
        RANK() OVER (PARTITION BY land ORDER BY geboortedatum ASC) AS oudste_rank,
        RANK() OVER (PARTITION BY land ORDER BY geboortedatum DESC) AS jongste_rank
    FROM wielrenner
)
SELECT land, naam, geboortedatum
FROM Ranking
WHERE oudste_rank = 1 OR jongste_rank = 1;
```

2. Welke wedstrijden hadden het hoogste gemiddelde snelheid per jaar?

Gebruik window-functies om de snelste wedstrijd per jaar te bepalen.
```sql
WITH WedstrijdSnelheid AS (
    SELECT 
        wedstrijdnaam, datum, gemiddelde_snelheid,
        RANK() OVER (PARTITION BY EXTRACT(YEAR FROM datum) ORDER BY gemiddelde_snelheid DESC) AS snelste_rank
    FROM wedstrijd
)
SELECT wedstrijdnaam, datum, gemiddelde_snelheid
FROM WedstrijdSnelheid
WHERE snelste_rank = 1;
```

3. Combineer wielrenners uit Nederland en België zonder duplicaten.

Gebruik een set-operator om wielrenners te combineren.

```sql
SELECT naam, land
FROM wielrenner
WHERE land = 'Nederland'
UNION
SELECT naam, land
FROM wielrenner
WHERE land = 'België';
```

4. Welke wielrenners hebben deelgenomen aan een wedstrijd, maar nog nooit gewonnen?

Gebruik set-operatoren zoals EXCEPT.

```sql
SELECT wielrennerid
FROM wedstrijddeelname
EXCEPT
SELECT wielrennerid
FROM overwinning;
```

5. Vind de top 3 wielrenners met de meeste overwinningen in 2023.

Gebruik een combinatie van WITH AS en aggregatie.

```sql
WITH Overwinningen2023 AS (
    SELECT 
        w.naam, COUNT(*) AS aantal_overwinningen
    FROM overwinning o
    JOIN wielrenner w ON o.wielrennerid = w.wielrennerid
    JOIN wedstrijd wed ON o.wedstrijdid = wed.wedstrijdid
    WHERE EXTRACT(YEAR FROM wed.datum) = 2023
    GROUP BY w.naam
)
SELECT naam, aantal_overwinningen
FROM Overwinningen2023
ORDER BY aantal_overwinningen DESC
LIMIT 3;
```

6. Selecteer de wielrenners die in minstens 10 verschillende wedstrijden hebben deelgenomen.

Gebruik groepering en een HAVING-clausule.

```sql
SELECT w.naam, COUNT(DISTINCT wd.wedstrijdid) AS aantal_wedstrijden
FROM wielrenner w
JOIN wedstrijddeelname wd ON w.wielrennerid = wd.wielrennerid
GROUP BY w.naam
HAVING COUNT(DISTINCT wd.wedstrijdid) >= 10;
```

7. Bereken de gemiddelde afstand per land voor alle gereden wedstrijden.

Gebruik aggregatie.

```sql
SELECT w.land, AVG(wed.afstand) AS gemiddelde_afstand
FROM wielrenner w
JOIN wedstrijddeelname wd ON w.wielrennerid = wd.wielrennerid
JOIN wedstrijd wed ON wd.wedstrijdid = wed.wedstrijdid
GROUP BY w.land;
```

8. Geef de derde tot vijfde wielrenner met de meeste deelnames weer.

Gebruik OFFSET en FETCH NEXT.

```sql
SELECT w.naam, COUNT(*) AS aantal_deelnames
FROM wedstrijddeelname wd
JOIN wielrenner w ON wd.wielrennerid = w.wielrennerid
GROUP BY w.naam
ORDER BY aantal_deelnames DESC
OFFSET 2 FETCH NEXT 3 ROWS ONLY;
```

9. Welke wielrenners hebben zowel wedstrijden in 2022 als 2023 gewonnen?

Gebruik INTERSECT.

```sql
SELECT o.wielrennerid
FROM overwinning o
JOIN wedstrijd wed ON o.wedstrijdid = wed.wedstrijdid
WHERE EXTRACT(YEAR FROM wed.datum) = 2022
INTERSECT
SELECT o.wielrennerid
FROM overwinning o
JOIN wedstrijd wed ON o.wedstrijdid = wed.wedstrijdid
WHERE EXTRACT(YEAR FROM wed.datum) = 2023;
```

10. Wat is het percentage gewonnen wedstrijden per wielrenner?

Gebruik window-functies om het totaal en het percentage per wielrenner te berekenen.

```sql
WITH TotaalDeelnames AS (
    SELECT 
        w.wielrennerid, w.naam, COUNT(*) AS totaal_wedstrijden
    FROM wielrenner w
    JOIN wedstrijddeelname wd ON w.wielrennerid = wd.wielrennerid
    GROUP BY w.wielrennerid, w.naam
),
TotaalOverwinningen AS (
    SELECT 
        o.wielrennerid, COUNT(*) AS totaal_overwinningen
    FROM overwinning o
    GROUP BY o.wielrennerid
)
SELECT 
    d.naam,
    d.totaal_wedstrijden,
    COALESCE(o.totaal_overwinningen, 0) AS totaal_overwinningen,
    ROUND(COALESCE(o.totaal_overwinningen, 0) * 100.0 / d.totaal_wedstrijden, 2) AS winstpercentage
FROM TotaalDeelnames d
LEFT JOIN TotaalOverwinningen o ON d.wielrennerid = o.wielrennerid;
```
