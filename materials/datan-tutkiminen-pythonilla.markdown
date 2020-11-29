---
layout: default
title: Datan tutkiminen Pythonilla
parent: Materiaalit Suomeksi
nav_order: 7
---

# Datan tutkiminen Pythonilla

Voit ladata materiaalin [tästä Jupyter Notebookina]({{ OSlevelUPkoodarit.github.io }}{% link /notebooks/Data_exploring.ipynb %})
{: .fs-6 }


## Datan käsitteleminen Pythonilla

Python on kieli, jota on alunperin käytetty skriptaamiseen eli luomaan koodia, joka suorittaa pieniä tehtäviä tietokoneella. Nykyisin Pythonia voidaan käyttää skriptaamisen lisäksi myös web-ohjelmointiin ja data science -tekemiseen, joten se on hyvin monipuolinen kieli.

Python ei itsessään ole tehokas ohjelmointikieli, mutta sen tarjoamat kirjastot datan käsittelyyn pohjautuvat C-ohjelmointikieleen, mikä nopeuttaa ohjelmien suoritusaikaa suurilla datamassoilla. Lisäksi se on helpompi yhdistää olemassa oleviin järjestelmiin monipuolisuutensa ansiosta ja saattaa olla helpompi ottaa käyttöön jo valmiiksi ohjelmointia osaaville. Pythonin lisäksi R on suosittu. 

## Pandas
Pandas on kirjasto, jota käytetään usein datan tutkimiseen ja siivoamiseen. Se on toteutettu C-ohjelmointikielellä, mikä tekee siitä suoritusajaltaan tehokkaan. Se tarjoaa hyvät tietorakenteet datan käsittelyyn ja sisältää monia hyviä funktioita, jotka tekevät ohjelmoinnista nopeaa ja mutkatonta. Pandasin tietorakenteista käytetyimpiä ovat [Dataframe ja Series -tietorakenteet](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.DataFrame.html). Pandasin tietotyypit eroavat myös hieman Pythonin perinteisistä tietotyypeistä.

| Python | Pandas |Merkitys|
|--------|:-------:|-------:|
|str|object|Teksti|
|int |int64 | Kokonaisluku|
|float|float64|Liukuluku|
|bool|bool|Totuusarvo|
|datetime|datetime64|Päivämäärä kellonajalla|
|datetime.timedelta|timedelta|Kuvaa päiviä, tunteja, minuutteja, sekunteja|
|Ei ole Pythonissa|category|Kategoria|

## Series 
Series on rivi, jolla on otsikot. Yksi Series voi sisältää eri tyyppistä dataa ja otsikoihin viitataan nimellä index. Seriesin voi luoda dictionarysta, ndarraysta tai skalaarista.



```python
import pandas as pd
import numpy as np

#Dictonary, keys define indeces in Series
dict_data={'A': 1, 'B': 2, 'C':3}

dict_series=pd.Series(dict_data)

print(dict_series)
```

    A    1
    B    2
    C    3
    dtype: int64



```python
## ndarray, we need to define indeces separately
array_data=np.random.random(3)
indeces=['A', 'B', 'C']

array_series=pd.Series(array_data, index=indeces)

print(array_series)
```

    A    0.301430
    B    0.786559
    C    0.777387
    dtype: float64



```python
indeces=['A', 'B', 'C']
scalar_series=pd.Series(3, index=indeces)

print(scalar_series)
```

    A    3
    B    3
    C    3
    dtype: int64


Mitä tapahtuu, jos datan arvojen tyyppejä vaihdetaan? Jos esimerkiksi dictionaryn arvoista johonkin vaihdetaan merkkijono? Entä jos index-taulukossa on enemmän arvoja kuin dictionaryssa? KOKEILLAAN!

### Dataframe

Dataframe on matriisin kaltainen tietorakenne. Siinä on siis rivejä ja sarakkeita, ja sarakkeilla on otsikot. Eri sarakkeissa voi olla eri tyyppistä dataa, mutta yhdessä sarakkeessa olevat arvot tulisi olla aina samantyyppisiä. Dataframen voi ajatella olevan kuin suuri joukko Series-rivejä, joilla on yhteinen otsikko. Monet Dataframen funktiot palauttavatkin Series-rivin.

Dataframen voi luoda esimerkiksi
* dictionarysta, joka sisältää yksiulotteisia ndarrayta, listoja, dictionaryja tai Series-rivejä
* kaksiulotteisesta Numpyn ndarraysta
* toisesta Dataframesta

Tässä tapauksessa ne eivät ole kiinnostavia, koska data luetaan yleensä tiedostosta tai tietokannasta. Datan voi lukea csv-tiedostosta dataframeen käyttämällä pandasin funktiota *read_csv*:

```
df=pd.read_csv('path/to/file.csv')
```

## Datan importtaaminen ja tutkiminen

Luetaan ensin data sisään tiedostosta. Kyseinen tiedosto sisältää keinotekoista dataa, ja voit luoda sen itsellesi ajamalla tietokoneellasi [tämän Jupyter Notebookin ]({{ OSlevelUPkoodarit.github.io }}{% link notebooks/dataset_generator.ipynb %}).


```python
df=pd.read_csv('generated_dataset.csv', sep=';')
```

df on muuttuja, johon tieto tallennetaan ja read_csv funktiolle annetaan parametriksi tässä tapauksessa tiedoston sijainti ja mitä erotinmerkkiä tiedostossa on käytetty. Valinnaisia parametreja on enemmänkin, esimerkiksi jos vain osa sarakkeista tai riveistä haluttaisiin lukea.

Tutkitaan seuraavaksi, kuinka monta riviä ja saraketta datasetissä on. Tämä tieto saadaan DataFramen shape-attribuutista.


```python
df.shape
```




    (1000, 7)



Data sisältää siis 1000 riviä ja 7 saraketta.
Haetaan seuraavaksi datan n ensimmäistä riviä kutsumalla funktiota *head*. Funktio ottaa parametriksi rivien lukumäärän n, joka halutaan hakea. Jos mitään parametriä ei anneta, haetaan 5 riviä.


```python
df.head(10)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Student_id</th>
      <th>First_name</th>
      <th>Last_name</th>
      <th>Points</th>
      <th>Enrolled</th>
      <th>Age</th>
      <th>Gender</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>10000</td>
      <td>Pertti</td>
      <td>Sanchez</td>
      <td>265</td>
      <td>0</td>
      <td>35.0</td>
      <td>Female</td>
    </tr>
    <tr>
      <th>1</th>
      <td>10001</td>
      <td>Emily</td>
      <td>Atkins</td>
      <td>17</td>
      <td>1</td>
      <td>30.0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>10002</td>
      <td>Sanna</td>
      <td>Atkins</td>
      <td>291</td>
      <td>1</td>
      <td>32.0</td>
      <td>Female</td>
    </tr>
    <tr>
      <th>3</th>
      <td>10003</td>
      <td>Outi</td>
      <td>Sanchez</td>
      <td>273</td>
      <td>1</td>
      <td>35.0</td>
      <td>Female</td>
    </tr>
    <tr>
      <th>4</th>
      <td>10004</td>
      <td>Dina</td>
      <td>Smith</td>
      <td>273</td>
      <td>0</td>
      <td>34.0</td>
      <td>Female</td>
    </tr>
    <tr>
      <th>5</th>
      <td>10005</td>
      <td>Liisa</td>
      <td>Nieminen</td>
      <td>245</td>
      <td>0</td>
      <td>35.0</td>
      <td>Female</td>
    </tr>
    <tr>
      <th>6</th>
      <td>10006</td>
      <td>Liisa</td>
      <td>Virtanen</td>
      <td>230</td>
      <td>0</td>
      <td>NaN</td>
      <td>Female</td>
    </tr>
    <tr>
      <th>7</th>
      <td>10007</td>
      <td>Dina</td>
      <td>Laine</td>
      <td>285</td>
      <td>0</td>
      <td>28.0</td>
      <td>Other</td>
    </tr>
    <tr>
      <th>8</th>
      <td>10008</td>
      <td>Emily</td>
      <td>Ruiz</td>
      <td>215</td>
      <td>1</td>
      <td>25.0</td>
      <td>Other</td>
    </tr>
    <tr>
      <th>9</th>
      <td>10009</td>
      <td>Pertti</td>
      <td>Smith</td>
      <td>241</td>
      <td>1</td>
      <td>38.0</td>
      <td>Other</td>
    </tr>
  </tbody>
</table>
</div>



Seuraavaksi tutkitaan, mitä datatyyppejä datasetti sisältää. Se tieto saadaan DataFramen dtypes-attribuutista.


```python
df.dtypes
```




    Student_id      int64
    First_name     object
    Last_name      object
    Points          int64
    Enrolled        int64
    Age           float64
    Gender         object
    dtype: object



Tarkastellaan, millaisia arvoja numeeriset sarakkeet saavat.


```python
df.describe()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Student_id</th>
      <th>Points</th>
      <th>Enrolled</th>
      <th>Age</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>1000.000000</td>
      <td>1000.000000</td>
      <td>1000.000000</td>
      <td>952.000000</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>10499.500000</td>
      <td>154.029000</td>
      <td>0.488000</td>
      <td>33.381303</td>
    </tr>
    <tr>
      <th>std</th>
      <td>288.819436</td>
      <td>85.183381</td>
      <td>0.500106</td>
      <td>6.236370</td>
    </tr>
    <tr>
      <th>min</th>
      <td>10000.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>16.000000</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>10249.750000</td>
      <td>85.750000</td>
      <td>0.000000</td>
      <td>29.000000</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>10499.500000</td>
      <td>153.000000</td>
      <td>0.000000</td>
      <td>33.000000</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>10749.250000</td>
      <td>228.250000</td>
      <td>1.000000</td>
      <td>37.000000</td>
    </tr>
    <tr>
      <th>max</th>
      <td>10999.000000</td>
      <td>300.000000</td>
      <td>1.000000</td>
      <td>55.000000</td>
    </tr>
  </tbody>
</table>
</div>



Ja myös kategorisia muuttujia voidaan tarkastella, luettelemalla niiden kaikki arvot ja määrät:


```python
df['Gender'].value_counts()
```




    Male      329
    Other     316
    Female    303
    Name: Gender, dtype: int64



Aiemmasta taulukosta, jossa näytetään ensimmäisen 5 rivin tietoja, näkyy 'NaN'-arvoja. Haluamme seuraavaksi tutkia, kuinka monta puuttuvaa arvoa eri sarakkeista löytyy.


```python
df.isna().sum()
```




    Student_id     0
    First_name     0
    Last_name      0
    Points         0
    Enrolled       0
    Age           48
    Gender        52
    dtype: int64



Mietitäänpä tarkemmin mitä ylempänä tapahtuu. df on DataFrame-tyyppinen muuttuja. DataFramella on funktio *isna*. joka palauttaa uuden DataFramen, joka sisältää jokaiselle arvolle DataFramessa tiedon siitä, onko kyseessä puuttuva arvo. Isna-funktion palauttamalle DataFramelle voidaan kutsua *sum*-funktiota, joka tässä tapauksessa laskee yhteen sarakkeessa esiintyvien True-arvojen määrän. Jos sarakkeissa olisi lukuja, se laskisi niiden summan.

Seuraavaksi voidaan tehdä muutama harjoitus. Se tapahtuu lataamalla omalle tietokoneelle [tämä Jupter Notebook]({{ OSlevelUPkoodarit.github.io }}{% link /notebooks/Python_exercise.ipynb %}). Tähän teoriaosuuteen liittyy kyseisen notebookin osio 1.


