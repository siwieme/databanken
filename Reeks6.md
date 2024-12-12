# SQL Features from Presentation 6 (Reeks 6)

## OFFSET en FETCH
### Wat is het?
- **OFFSET**: Hiermee geef je aan hoeveel rijen uit het resultaat moeten worden overgeslagen.
- **FETCH**: Hiermee geef je aan hoeveel rijen van het resultaat moeten worden opgehaald.

### Voorbeelden
1. **Sla de eerste 5 rijen over en haal vervolgens 10 rijen op:**
   ```sql
   SELECT naam, geboortedatum
   FROM wielrenner
   ORDER BY geboortedatum DESC
   OFFSET 5 FETCH FIRST 10 ROWS ONLY;
   ```
2. **Gebruik FETCH WITH TIES om extra rijen met dezelfde waarde als de laatste rij mee te nemen:**
   ```sql
   SELECT naam, gewicht
   FROM wielrenner
   ORDER BY gewicht DESC
   FETCH FIRST 3 ROWS WITH TIES;
   ```

## Set-operatoren

### Wat is het?

- **UNION**: Combineert resultaten van twee queries en verwijdert dubbele waarden.
- **INTERSECT**: Geeft alleen gemeenschappelijke rijen van twee queries terug.
- **EXCEPT**: Geeft rijen terug die alleen in de eerste query voorkomen.

### Voorbeelden
1. **UNION:**: Fietsers uit België of met een gewicht onder 70 kg:
   ```sql
   SELECT naam
   FROM wielrenner
   WHERE landcode = 'BE'
   UNION
   SELECT naam
   FROM wielrenner
   WHERE gewicht < 70;
   ```
2. **INTERSECT**: Fietsers die zowel uit België komen als minder dan 70 kg wegen:
   ```sql
   SELECT naam
   FROM wielrenner
   WHERE landcode = 'BE'
   INTERSECT
   SELECT naam
   FROM wielrenner
   WHERE gewicht < 70;
   ```
3. **EXCEPT**: Fietsers uit België die niet minder dan 70 kg wegen:
   ```sql
   SELECT naam
   FROM wielrenner
   WHERE landcode = 'BE'
   EXCEPT
   SELECT naam
   FROM wielrenner
   WHERE gewicht < 70;
   ```

## WINDOW-functies

### Wat is het?

* WINDOW-functies voeren berekeningen uit over een groep rijen (een venster) zonder de resultaten samen te vatten.

### Veelgebruikte functies

1. **ROW_NUMBER()**: Geeft een uniek nummer aan elke rij in het resultaat.
2. **RANK()**: Geeft een rangnummer aan elke rij in het resultaat.
3. **DENSE_RANK()**: Geeft een rangnummer aan elke rij in het resultaat zonder gaten.
4. **LEAD()**: Geeft de waarde van een rij verderop in het resultaat.
5. **LAG()**: Geeft de waarde van een rij eerder in het resultaat.

### Voorbeelden

1. **Rangschik fietsers op gewicht**: 
   ```sql
   SELECT naam, gewicht,
          RANK() OVER (ORDER BY gewicht DESC) AS rank
   FROM wielrenner;
   ```
2. **Gemiddeld gewicht per land**:
    ```sql
    SELECT landcode, naam, gewicht,
             AVG(gewicht) OVER (PARTITION BY landcode) AS avg_weight
    FROM wielrenner;
    ```
3. **Vergelijk een gewicht met dat van de vorige rij**:
    ```sql
    SELECT naam, gewicht,
           LAG(gewicht) OVER (ORDER BY gewicht) AS previous_weight
    FROM wielrenner;
    ```

## WITH-queries

### Wat is het?

Met `WITH` kun je tijdelijke tabellen definiëren die in een query kunnen worden gebruikt. Dit maakt complexe queries overzichtelijker.

### Toepassingen

1. **Eenvoudige Common Table Expressions (CTEs)**:
    ```sql
    WITH leeftijdsgroepen AS (
        SELECT naam, geboortedatum, 
            AGE(CURRENT_DATE, geboortedatum) AS leeftijd
        FROM wielrenner
    )
    SELECT naam, leeftijd
    FROM leeftijdsgroepen
    WHERE leeftijd > '30 years';
    ```
2. **Recursieve queries**: Toon een hiërarchie van fietsers en teams
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