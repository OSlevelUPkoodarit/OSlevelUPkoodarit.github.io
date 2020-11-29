---
layout: default
title: Versionhallinta ja Git
parent: Materiaalit Suomeksi
nav_order: 2
---

# Versionhallinta ja Git

## Mikä on versionhallinta?

Versionhallinta tarkoittaa palvelua, joka säilöö koodia. Joiltain osin koodin versionhallinta toimii hieman samassa hengessä, kuin monille tutut Dropbox tai Google Drive, joihin voi tallentaa tiedostoja ja niiden eri versioita. Moni on varmaan käyttänyt myös esim. Overleafia opinnäytetöiden yms. tekstitiedostojen versionhallintaan. Kaikkien näiden etu on se, että samasta tiedostosta tai ohjelmasta voi säilyttää varmuuskopioita sekä nykyisestä, että aiemmista versioista. Jos omalta koneelta katoaa kaikki tiedostot, ne säilyvät silti jossain, mistä ne on mahdollista palauttaa.

Puhutaan tässä yhteydessä erityisesti koodiin liittyvästä versionhallinnasta. Sen käyttöön on pääasiassa motiivina varmuuskopiointi, koodin jakaminen muille, sekä muiden projekteihin osallistuminen ja ryhmätyöskentelyn helpottaminen. Lisäksi versionhallintatyökalujen avulla on mahdollista merkitä jokin projektin tila sellaiseksi, että siihen voidaan halutessa palata myöhemmin. Koodatessa tämä onkin hyödyllistä, sillä monesti esim. uusia ominaisuuksia rakenneltaessa joudutaan kokeilemaan monia eri vaihtoehtoja, joista jotkut saattavat osoittautua huonoiksi ratkaisuiksi, ja helposti saatetaan haluta palata takaisin aikaisempaan toimivaan versioon. Versionhallinnan avulla voidaan nähdä, miten ohjelman kehitys on edistynyt ja kenen toimesta mikäkin muutos on tehty.

## Mikä on Git?

Git on eräs monista työkaluista versionhallintaan. Git on saavuttanut suosiota koodareiden ja yritysten keskuudessa, sillä se tarjoaa hyvät ja monipuoliset työkalut etänä ryhmässä työskentelyyn, sillä kehittäjien on mahdollista nähdä ja muokata toistensa koodia, nähdä koko projektin kehityshistoria, antaa muutoksista palautetta ja tehdä vaikkapa bugi-ilmoituksia. Gittiä voi käyttää joko komentoriviltä tai pluginien avulla graafisella käyttöliittymällä. Isoimpana erona joihinkin muihin versionhallintatyökaluihin on se, miten git käsittelee dataa ja versioita. Git ei taltioi pelkkiä muutoksia tiedostoista, vaan “snapshotteja” eri hetkistä. Jokainen commit on sen hetkinen tila jokaisesta tiedostosta hakemistossa. Eri versiot ovat siis oikeasti eri ajanhetkien tilanteita samasta hakemistosta.

## Tiedoston kolme tilaa

Tiedostoilla on gitissä kolme tärkeää tilaa: **committed**, **modified** ja **staged**.

Commit on gitin käytön kannalta yksi tärkeimmistä konsepteista, sillä tietoa tallennetaan git-projektiin committeina. Committia voi ajatella eräänlaisena pakettina tehtyjä muutoksia. Tiedoston tila committed tarkoittaa siis, että tiedosto on tallennettu lokaaliin kantaan sellaisenaan kuin se sillä hetkellä on.

Modified tarkoittaa, että tiedostoon on tehty muutoksia, joita ei ole vielä tallennettu lokaaliin git-kantaan. Staged tarkoittaa, että muokattu tiedosto on merkitty tallennettavaksi seuraavassa commitissa lokaaliin kantaan nykyisessä muodossaan.

## Git projektin rakenne

Git projektilla on hieman vastaavanlainen kolmijako: **working directory**, **staging area** ja **git directory**. Tässä kohtaa on tärkeää ymmärtää ero näiden välillä. Working directory on käytännössä tietokoneen levylle tallennetut tiedostot. Git directory on puolestaan lokaaliin git-kantaan tallennetut tiedostot, “local repository”. Gitiä voi siis ajatella ikään kuin omana erillisenä tiedostojärjestelmänään. Staging area on osa git directorya, joka pitää kirjaa siitä, mitkä muutokset on merkitty tallennettavaksi seuraavassa commitissa.

## Git-projektin aloittaminen

Git-projektia aloittaessa git hakemisto (lokaali kanta) alustetaan projektille ajamalla projektikansiossa komento:

```
git init
```

Tämän jälkeen kansion sisällä on mahdollista suorittaa muita git-komentoja.

## Commitin luominen

Kun koodiin tehdään muutoksia, muutetut tiedostot vaihtuvat tilaan modified. Committeja käytetään ikään kuin checkpointeina, joihin voi palata jos joku menee pieleen. Monesti ohjelmaa koodatessa esimerkiksi jonkin uuden toiminnallisuuden lisääminen voitaisiin paketoida uutena committina.

Commit aloitetaan ajamalla komento git add joka vaihtaa muokattujen tiedostojen tilaksi staged (eli ne on merkattu tallennettavaksi seuraavassa commitissa, mutta eivät vielä ole tallennettuina lokaaliin kantaan). Kaikkia muutettuja tiedostoja ei tarvitse lisätä, jolloin niiden sisältämiä muutoksia ei tallenneta kyseiseen committiin (vaikka ne ovat toki tallennettuina lokaalisti oman koneen hakemistossa). Kun kaikki halutut muutokset ovat staging tilassa,ajetaan commitin luova komento git commit, joka yhdistää kaikki stagingissa olevat muutokset yhdeksi commitiksi, eli toisin sanottuna vaihtaa tiedostot tilaan committed. Tällöin tiedostot on tallennettu lokaaliin git-kantaan muokatussa muodossaan.

Commitilla paketoidaan kasa tehtyjä muutoksia uudeksi versioksi, joten commit tarvitsee aina jonkun viestin, jolla kerrotaan mitä kyseisten muutosten on tarkoitus tehdä. Näin versiohistoriaa myöhemmin tutkimalla on helpompi nähdä, mitä missäkin vaiheessa on tehty ja mikä sen tarkoitus on ollut. Viesti lisätään commit-komennon yhteydessä seuraavalla tavalla:

```
git commit -m "kuvaava otsikko".
```

Tässä vaiheessa kaikki muutokset ovat kuitenkin vielä lokaalisti omalla koneella, joten jos kone nyt jostain syystä vaikkapa varastettaisiin tai tuhoutuisi,nämä muutokset menetettäisiin.

Normaali git-flow on siis myös n. kolmivaiheinen:

1. Tiedostoja muokataan editorissa ja tallennetaan tietokoneen levylle (working directory)
2. Tiedostot merkitään tallennettaviksi muokatussa muodossa seuraavan commitin yhteydessä (staging)
3. Tiedostot tallennetaan pysyvästi lokaaliin git-kantaan sellaisinaan, kun ne ovat stagingissa olleet.

Jos tiedostoja lisätään komennolla `git add` stagingiin, mutta muokataan uudelleen ennen committia, muokatut tiedostot lisätään taas uudestaan stagingiin jos ne halutaan mukaan committiin. Erittäin hyödyllinen komento on `git status`. Sen avulla on mahdollista seurata tiedostojen tilaa, ja tarkistaa mitkä tiedostot ovat päätymässä committiin, ja mitkä jäämässä pois.

## Etärepositorio, Local ja Remote

Jotta koodi on jaettavissa esim. Githubin kautta, projektille pitää luoda etärepositorio, joka liitetään omaan lokaaliin git-projektiin. Tämä tapahtuu lisäämällä repo Git-projektin etärepositorioksi, eli remoteksi. Kun Git-projektille lisätään etärepositorio, on mahdollista siirtää tietoa sen ja omalla koneella olevan projektin välillä. Tällöin projektista on olemassa kaksi versiota: paikallinen (local), eli omalla koneella oleva projekti ja etärepositorion versio (remote), eli esim. GitHubissa oleva versio. Etärepositorio yhdistetään paikalliseen projektiin komennolla:

```
git remote add <remoten nimi> <remoten osoite>
```

Kun remote on lisätty projektille, voidaan luoda projektista toinen versio myös remote repositorioon ajamalla:

```
git push <remotennimi> <haarannimi>
```

Palaamme haaroihin tarkemmin myöhemmissä osissa. Nyt tiedostot ja niiden muutoshistoria on palautettavissa miltä tahansa koneelta (joilla on hakemistoon oikeus). Näin oma koodi on mahdollista jakaa myös muille kehittäjille. Muutokset voitaisiin hakea samalle tai toiselle koneelle komennolla

```
git pull
```

Tällöin haetaan hakemiston viimeisimmät muutokset. Jos aloitettaisiin projektin työstäminen kokonaan uudelta koneelta, eikä kyseistä hakemistoa olisi vielä koskaan sillä koneella ollutkaan, käyttäisimme komentoa

```
git clone <repon osoite>
```

joka kloonaisi olemassa olevan hakemiston tälle koneelle.

## Lähteet

- [Gitin oma materiaali](https://git-scm.com/book/en/v1/Getting-Started-Git-Basics)
- [Helsingin yliopiston lapiokurssi (Tietokone työvälineenä)](https://tkt-lapio.github.io/git/)