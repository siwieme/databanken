# Summary of SQL Techniques from Presentations

## Aggregation and Grouping
**Key Concepts:**

- Aggregation functions: COUNT, AVG, SUM, MIN, MAX.
- GROUP BY to group data.
- HAVING to filter groups.

**Examples:**

```sql
SELECT type, COUNT(*) AS aantal
FROM rit
GROUP BY type;
```

```sql
SELECT moeilijkheid, AVG(afstand) AS gemiddelde_afstand
FROM route
GROUP BY moeilijkheid;
```

## Date and Time Manipulation
**Key Functions:**

- `NOW()` and `CURRENT_DATE` for current timestamp/date.
- `AGE()` for differences.
- `DATE_PART()` to extract date components.

**Examples:**

```sql
SELECT naam, AGE(CURRENT_DATE, geboortedatum) AS leeftijd
FROM wielrenner;
```

## Window Functions
**Key Features:**

- Calculations over a "window" of rows.
- Common functions: RANK(), ROW_NUMBER(), AVG() OVER.

**Examples:**

```sql
SELECT naam, gewicht, RANK() OVER (ORDER BY gewicht DESC) AS rank
FROM wielrenner;
```

## Set Operators
**Combine query results:** UNION, INTERSECT, EXCEPT.

**Examples:**

```sql
SELECT naam FROM wielrenner WHERE landcode = 'BE'
UNION
SELECT naam FROM wielrenner WHERE gewicht < 70;
```

```sql
SELECT naam FROM wielrenner WHERE landcode = 'BE'
INTERSECT
SELECT naam FROM wielrenner WHERE gewicht < 70;
```

## Recursive Queries
**Hierarchical relationships:**

```sql
WITH RECURSIVE team_hierarchy AS (
    SELECT naam, teamnaam
    FROM wielrenner
    WHERE naam = 'Renner1'
    UNION
    SELECT w.naam, w.teamnaam
    FROM wielrenner w
    INNER JOIN team_hierarchy th ON w.teamnaam = th.naam
)
SELECT * FROM team_hierarchy;
```

---
