
# PostgreSQL Practice Exercises

## Exercises from Presentation 4
### Total Number of Races
**Task:** Count the total number of races.

```sql
SELECT COUNT(*) AS total_races FROM rit;
```

### Average Distance of Routes by Difficulty
**Task:** Calculate average distance for difficulty levels.

```sql
SELECT moeilijkheid, AVG(afstand) AS average_distance
FROM route
GROUP BY moeilijkheid;
```

## Exercises from Presentation 5
### Cyclist Ages

```sql
SELECT naam, AGE(CURRENT_DATE, geboortedatum) AS age
FROM wielrenner;
```

## Overarching Exercises
### Combined Query with Aggregates
**Task:** For each country, rank cyclists by weight.

```sql
SELECT landcode, naam, gewicht,
       AVG(gewicht) OVER (PARTITION BY landcode) AS avg_weight,
       RANK() OVER (PARTITION BY landcode ORDER BY gewicht DESC) AS rank
FROM wielrenner;
```

### Date and Set Operations
**Task:** Cyclists born before 1990 who raced in 2020.

```sql
SELECT DISTINCT w.naam
FROM wielrenner w
JOIN uitslag u ON w.naam = u.rennernaam
JOIN rit r ON u.wedstrijdnaam = r.wedstrijdnaam
WHERE w.geboortedatum < '1990-01-01'
  AND DATE_PART('year', r.datum) = 2020;
```
