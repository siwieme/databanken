
# Additional PostgreSQL Practice Exercises

## Exercises from Presentation 4 (Aggregation and Grouping)
### 1. Total Race Count by Type
**Task:** Count the total number of races grouped by type.

```sql
SELECT type, COUNT(*) AS total_races
FROM rit
GROUP BY type;
```

### 2. Maximum Route Distance
**Task:** Find the maximum distance (`afstand`) in the `route` table.

```sql
SELECT MAX(afstand) AS max_distance
FROM route;
```

### 3. Difficulty Levels with High Average Altitude
**Task:** Identify difficulty levels where the average altitude gain (`hoogtemeters`) exceeds 500.

```sql
SELECT moeilijkheid, AVG(hoogtemeters) AS avg_altitude
FROM route
GROUP BY moeilijkheid
HAVING AVG(hoogtemeters) > 500;
```

## Exercises from Presentation 5 (Date and Time)
### 1. Cyclists Born in a Specific Month
**Task:** List all cyclists born in July.

```sql
SELECT naam
FROM wielrenner
WHERE DATE_PART('month', geboortedatum) = 7;
```

### 2. Time Between Race Dates
**Task:** Calculate the time interval between the earliest and latest race dates.

```sql
SELECT MIN(datum) AS earliest_date, MAX(datum) AS latest_date, MAX(datum) - MIN(datum) AS interval
FROM rit;
```

### 3. Extract Day of the Week for Races
**Task:** Retrieve the day of the week for each race.

```sql
SELECT wedstrijdnaam, TO_CHAR(datum, 'Day') AS race_day
FROM rit;
```

## Exercises from Presentation 6 (Advanced Queries)
### 1. Average Cyclist Weight by Team
**Task:** Compute the average weight (`gewicht`) of cyclists grouped by team.

```sql
SELECT teamnaam, AVG(gewicht) AS avg_weight
FROM wielrenner
GROUP BY teamnaam;
```

### 2. Top Cyclists by Weight in Each Country
**Task:** Rank cyclists by their weight within each country.

```sql
SELECT naam, landcode, gewicht, RANK() OVER (PARTITION BY landcode ORDER BY gewicht DESC) AS rank
FROM wielrenner;
```

### 3. Cyclists Participating in Multiple Competitions
**Task:** List cyclists who have participated in at least two different competitions.

```sql
SELECT rennernaam, COUNT(DISTINCT wedstrijdnaam) AS competition_count
FROM uitslag
GROUP BY rennernaam
HAVING COUNT(DISTINCT wedstrijdnaam) >= 2;
```

## Overarching Exercise
### Combining Grouping and Recursive Queries
**Task:** For each team, calculate the total weight of its cyclists and display the team hierarchy starting from the team with the heaviest cyclists.

```sql
WITH team_weights AS (
    SELECT teamnaam, SUM(gewicht) AS total_weight
    FROM wielrenner
    GROUP BY teamnaam
)
SELECT *
FROM team_weights
ORDER BY total_weight DESC;
```
