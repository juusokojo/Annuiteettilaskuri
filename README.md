# Annuiteettilaskuri

Yhden tiedoston autorahoituslaskuri. Avaa `index.html` selaimessa – ei riippuvuuksia eikä asennusta.

Laskuri ei pysähdy kuukausierään, koska kuukausierällä ei voi vertailla tarjouksia. Se laskee myös
kulut ja todellisen vuosikoron, joka on ainoa vertailukelpoinen luku.

## Syötteet

| Kenttä | Selitys |
| --- | --- |
| Ostohinta | Auton hinta euroina |
| Käsiraha | Itse maksettava osuus; rahoitettava summa on erotus |
| Viimeinen suurempi erä | Jäännösarvo prosentteina ostohinnasta |
| Lainan korko | Nimellinen vuosikorko |
| Maksuaika | Sopimuksen pituus kuukausina |
| Avausmaksu | Kertaluonteinen perustamiskulu |
| Tilinhoitomaksu | Laskutuslisä joka erässä |

## Tulokset

- Kuukausierä tilinhoitomaksuineen
- Laina-aikana maksettava korko euroina
- Todellinen vuosikorko
- Luottokustannukset yhteensä (korot ja kulut)
- Erittely, lyhennystaulukko ja huomautus siitä, montako prosenttiyksikköä kulut lisäävät

## Laskenta

Korko lasketaan jäljellä olevalle pääomalle, kuukausikorko on vuosikorko jaettuna kahdellatoista.
Kuukausierä ratkaistaan siitä, että erien ja viimeisen suuremman erän nykyarvo vastaa rahoitettavaa
summaa:

```
P = ostohinta − käsiraha
B = ostohinta × bullet-%
i = korko / 12 / 100
v = (1 + i)^(−n)

erä   = (P − B × v) × i / (1 − v)      nollakorolla (P − B) / n
korot = n × erä + B − P
```

Todellinen vuosikorko on korkokanta X, jolla kaikkien maksujen nykyarvo vastaa saatua lainaa.
Kaava noudattaa kuluttajaluottodirektiivin periaatetta: vuosittainen diskonttaus, aika vuosina.

```
P = avausmaksu + Σ (erä + tilinhoitomaksu) / (1+X)^(k/12) + B / (1+X)^(n/12),  k = 1…n
```

X ratkaistaan puolitushaulla, koska yhtälölle ei ole suljettua muotoa. Funktio on monotoninen X:n
suhteen, joten ratkaisu on yksikäsitteinen.

## Varmennus

Annuiteettikaava on tarkistettu kuukausi kuukaudelta -simulaatiolla: jäljellä oleva pääoma viimeisen
erän jälkeen vastaa jäännösarvoa ja kertynyt korko laskettua korkosummaa myös reunatapauksissa
(0 % korko, 0 % ja 99 % jäännösarvo). Todellisen vuosikoron ratkaisija on tarkistettu tapauksella,
jolla on suljettu muoto: 12 % nimellinen korko kuukausittain lyhennettynä antaa (1,01)^12 − 1 =
12,6825 %.

## Rajaukset

Laskuri ei huomioi auton arvonalenemaa, viimeisen erän uudelleenrahoitusta, pakollisia vakuutuksia
eikä käteisalennusta. Jos saat halvemman hinnan maksamalla käteisellä, vertaa rahoituksen
kokonaishintaa käteishintaan, älä listahintaan.
