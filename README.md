# Annuiteettilaskuri

Yhden tiedoston annuiteettilainalaskuri autorahoituksen vertailuun. Avaa `index.html` selaimessa — ei riippuvuuksia eikä asennusta.

## Syötteet

| Kenttä | Selitys |
| --- | --- |
| Ostohinta | Rahoitettava summa euroina (käsirahan jälkeen) |
| Viimeinen suurempi erä | Jäännösarvo prosentteina ostohinnasta |
| Lainan korko | Nimellinen vuosikorko |
| Maksuaika | Sopimuksen pituus kuukausina |

## Tulokset

- Kuukausierän suuruus
- Laina-aikana maksettavan koron määrä euroina
- Viimeisen erän suuruus euroina, maksut yhteensä ja lyhennystaulukko

## Laskentakaava

Korko lasketaan jäljellä olevalle pääomalle, kuukausikorko on vuosikorko jaettuna kahdellatoista.
Kuukausierä ratkaistaan siitä, että erien ja viimeisen suuremman erän nykyarvo vastaa rahoitettavaa summaa:

```
i   = korko / 12 / 100
v   = (1 + i)^(-n)
B   = ostohinta × bullet-%
erä = (ostohinta − B × v) × i / (1 − v)

korot yhteensä = n × erä + B − ostohinta
```

Nollakorolla erä on `(ostohinta − B) / n`.

## Rajaukset

Laskuri ei huomioi avaus- ja tilinhoitomaksuja eikä todellista vuosikorkoa. Kulut nostavat rahoituksen
todellista hintaa usein enemmän kuin korkoprosentin desimaalit, joten vertaa tarjouksia todellisella
vuosikorolla.
