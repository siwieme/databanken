Hier zijn tien SQL-oefeningen op testniveau gebaseerd op een wielrennen-databank. De vragen zijn ontworpen om concepten zoals joins, aggregatie, subqueries en filters te oefenen.

Oefeningen Wielrennen Databank
	1.	Selecteer alle wielrenners die in 2021 geboren zijn.

SELECT naam, geboortedatum
FROM wielrenner
WHERE EXTRACT(YEAR FROM geboortedatum) = 2021;


	2.	Vind de naam en het aantal overwinningen van wielrenners die meer dan 5 wedstrijden hebben gewonnen.

SELECT w.naam, COUNT(*) AS aantal_overwinningen
FROM overwinning o
JOIN wielrenner w ON o.wielrennerid = w.wielrennerid
GROUP BY w.naam
HAVING COUNT(*) > 5;


	3.	Welke wielrenner heeft de meeste wedstrijden gereden in 2023?

SELECT w.naam, COUNT(*) AS aantal_wedstrijden
FROM wedstrijddeelname wd
JOIN wielrenner w ON wd.wielrennerid = w.wielrennerid
WHERE EXTRACT(YEAR FROM wd.datum) = 2023
GROUP BY w.naam
ORDER BY aantal_wedstrijden DESC
LIMIT 1;


	4.	Selecteer de wedstrijden met een gemiddelde snelheid boven de 40 km/h.

SELECT wedstrijdnaam, gemiddelde_snelheid
FROM wedstrijd
WHERE gemiddelde_snelheid > 40;


	5.	Vind het totaal aantal kilometers afgelegd door elke wielrenner in alle wedstrijden waaraan ze hebben deelgenomen.

SELECT w.naam, SUM(wed.afstand) AS totale_afstand
FROM wedstrijddeelname wd
JOIN wedstrijd wed ON wd.wedstrijdid = wed.wedstrijdid
JOIN wielrenner w ON wd.wielrennerid = w.wielrennerid
GROUP BY w.naam;


	6.	Welke wielrenners hebben op hun verjaardag een wedstrijd gewonnen?

SELECT w.naam, wed.wedstrijdnaam, w.geboortedatum
FROM overwinning o
JOIN wielrenner w ON o.wielrennerid = w.wielrennerid
JOIN wedstrijd wed ON o.wedstrijdid = wed.wedstrijdid
WHERE TO_CHAR(w.geboortedatum, 'MM-DD') = TO_CHAR(wed.datum, 'MM-DD');


	7.	Welke landen hebben het meeste aantal overwinningen?

SELECT land, COUNT(*) AS aantal_overwinningen
FROM overwinning o
JOIN wielrenner w ON o.wielrennerid = w.wielrennerid
GROUP BY land
ORDER BY aantal_overwinningen DESC;


	8.	Selecteer de wielrenner(s) met de snelste gemiddelde snelheid ooit in een wedstrijd.

SELECT w.naam, wed.wedstrijdnaam, wed.gemiddelde_snelheid
FROM wedstrijddeelname wd
JOIN wielrenner w ON wd.wielrennerid = w.wielrennerid
JOIN wedstrijd wed ON wd.wedstrijdid = wed.wedstrijdid
WHERE wed.gemiddelde_snelheid = (
    SELECT MAX(gemiddelde_snelheid)
    FROM wedstrijd
);


	9.	Welke wedstrijden hebben in elk van de afgelopen 3 jaar een winnaar gehad?

SELECT wed.wedstrijdnaam
FROM wedstrijd wed
JOIN overwinning o ON wed.wedstrijdid = o.wedstrijdid
WHERE EXTRACT(YEAR FROM wed.datum) IN (2021, 2022, 2023)
GROUP BY wed.wedstrijdnaam
HAVING COUNT(DISTINCT EXTRACT(YEAR FROM wed.datum)) = 3;


	10.	Welke wielrenner heeft het hoogste aantal tweede plaatsen in wedstrijden?

SELECT w.naam, COUNT(*) AS aantal_tweede_plaatsen
FROM podium p
JOIN wielrenner w ON p.wielrennerid = w.wielrennerid
WHERE p.positie = 2
GROUP BY w.naam
ORDER BY aantal_tweede_plaatsen DESC
LIMIT 1;

Datasetvereisten:
	1.	Tabel wielrenner: bevat wielrenners met wielrennerid, naam, geboortedatum, en land.
	2.	Tabel wedstrijd: bevat wedstrijden met wedstrijdid, wedstrijdnaam, datum, afstand, en gemiddelde_snelheid.
	3.	Tabel wedstrijddeelname: koppelt wielrenners aan wedstrijden met wielrennerid, wedstrijdid, en datum.
	4.	Tabel overwinning: bevat overwinningen met wielrennerid en wedstrijdid.
	5.	Tabel podium: bevat podiumplaatsen met wedstrijdid, wielrennerid, en positie.

Laat weten als je extra tabellen, relaties of details nodig hebt! 😊
