# Voorbeeldvragen

## Algemeen

1.	Zoek de jongste wielrenner
* Schrijf een query die de jongste wielrenner in de database teruggeeft.
* ```sql
  SELECT
    naam
  FROM
      wielrenner
  WHERE
      geboortedatum = (
          SELECT
              MAX(geboortedatum)
          FROM
              wielrenner
          );
  ```
2.	Transformeer de naam van een wielerwedstrijd
* Maak een query die de unieke namen van specifieke wielerwedstrijden in hoofdletters omzet. In dit geval: wedstrijdnamen die een '-' bevatten. Dit kan nuttig zijn om bijvoorbeeld naamsconsistentie te testen in de databank.
* ```sql
  SELECT
      DISTINCT CASE
          WHEN wedstrijdnaam ILIKE '%-%' THEN UPPER(wedstrijdnaam)
          ELSE wedstrijdnaam
      END AS wedstrijdnaam
  FROM
      rit;
  ```
3.	Zoek wielrenners uit een bepaald land
* Pas een query toe om alle wielrenners uit een specifiek land (bijvoorbeeld Nederland of België) te vinden. Voeg eventueel een extra filter toe om enkel wielrenners te tonen die op World Tour rijden.
* ```sql
  SELECT
      wr.naam,
      status
  FROM
      wielrenner wr
  INNER JOIN
      wielerteam wt
  ON
      wt.naam = wr.teamnaam
  WHERE
      wr.landcode LIKE 'BE'
      AND status LIKE 'World Tour';
    ```
4.	Top 3 snelste tijden van een wedstrijd
* Stel een query op die de drie snelste tijden weergeeft voor een specifieke wielerwedstrijd, gesorteerd op tijd. Dit kan helpen om subqueries en sorteerfuncties te oefenen.
* ```sql
  SELECT
      tijd,
      rennernaam
  FROM
      uitslag
  WHERE
      wedstrijdnaam LIKE 'Tour de France'
      AND tijd IS NOT NULL
  ORDER BY
      tijd DESC
  LIMIT 3;
  ``
5.	Leeftijdscategorieën van wielrenners
* Maak een query die wielrenners in leeftijdscategorieën indeelt (bijvoorbeeld 18-25, 26-35, enzovoort). Dit kan nuttig zijn om te oefenen met CASE statements in SQL.
* ```sql
  SELECT
      naam,
      EXTRACT('Year' FROM NOW()) - EXTRACT('Year' FROM geboortedatum::timestamp) AS leeftijd,
      CASE
          WHEN EXTRACT('Year' FROM NOW()) - EXTRACT('Year' FROM geboortedatum::timestamp) < 20 THEN '-20'
          WHEN EXTRACT('Year' FROM NOW()) - EXTRACT('Year' FROM geboortedatum::timestamp) < 30 THEN '20-30'
          WHEN EXTRACT('Year' FROM NOW()) - EXTRACT('Year' FROM geboortedatum::timestamp) < 40 THEN '30-40'
          ELSE '40+'
      END AS leeftijdscategorie
  FROM
      wielrenner;

## Reeks2

1.	Wielrenners Zonder Overwinningen
* Schrijf een query die alle wielrenners (met hun nationaliteit) weergeeft zonder enige overwinningen. Gebruik een LEFT JOIN op de uitslag tabel en filter met IS NULL om wielrenners zonder overwinningen te vinden.
* ```sql
  SELECT
      wr.naam AS naam,
      wr.landcode AS nationaliteit
  FROM
      wielrenner wr
  LEFT JOIN
      uitslag u
  ON
      wr.naam = u.rennernaam
  WHERE
      u.positie IS NULL
  ORDER BY
      wr.naam;
  ```
