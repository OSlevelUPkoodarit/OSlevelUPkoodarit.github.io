---
layout: default
title: Datan siivoaminen Pythonilla
parent: Materiaalit Suomeksi
nav_order: 8
---

# Datan siivoaminen Pythonilla

Voit ladata materiaalin [tästä Jupyter Notebookina]({{ OSlevelUPkoodarit.github.io }}{% link notebooks/Data_cleaning.ipynb %})
{: .fs-6 }

Jatketaan siitä, mihin jäätiin edellisessä Jupyter notebookissa Data_exploring.

Huomattiin, että ikä ja sukupuoli -sarakkeissa on puuttuvia arvoja. Jos dataa olisi suuret määrät, voitaisiin esimerkiksi pudottaa pois ne rivit, joilla on puuttuvia arvoja missään sarakkeessa. Ensin voisi olla tietysti hyvä tarkistaa, ettei puuttuvista arvoista löyty patternia, vaan että niiden puuttuminen on satunnaista. Emme kuitenkaan mene niin pitkälle tällä kertaa.

Tutkitaanpa kyseisiä sarakkeita vielä hieman tarkemmin. Luetaan tiedosto uudelleen sisään ja tutkitaan sen jälkeen ikäsaraketta. 


```python
import pandas as pd
import numpy as np

df=pd.read_csv('generated_dataset.csv', sep=';')
```


```python
df['Age'].describe()
```




    count    952.000000
    mean      33.381303
    std        6.236370
    min       16.000000
    25%       29.000000
    50%       33.000000
    75%       37.000000
    max       55.000000
    Name: Age, dtype: float64




```python
df['Age'].median()
```




    33.0



Erilaisten datan tunnuslukujen lisäksi dataa voidaan myös plotata matplotlib-kirjaston avulla. Piirretään ikä-sarakkeessa olevista arvoista histogrammi.


```python
import matplotlib.pyplot as plt

plt.xlabel('Ikä')
plt.ylabel('Lukumäärä')
plt.hist(df['Age'].dropna(), bins=32, range=(df['Age'].min(), df['Age'].max()))
plt.show()
```


![plot](/assets/output_5_0.png)


Ikädata näyttää melko normaalisti jakautuneelta. Helppo ratkaisu lisätä puuttuvat arvot on esimerkiksi korvata ne keskiarvolla tai mediaanilla, jotka tässä tapauksessa ovat siis melko samat. Valitaan näistä keskiarvo ja korvataan kaikki puuttuvat arvot sillä *fillna*-funktion avulla:


```python
df['Age']=df['Age'].fillna(df['Age'].mean())
```

Sitten on vuorossa sukupuolisarake. Sukupuoli onkin hieman mutkikkaampi. Kyseessä on kategorinen muuttuja, joka saattaa olla pääteltävissä esimerkiksi etunimen perusteella, mutta ei aina. Etunimenkään perusteella päättelemistä ei voi automatisoida.


```python
df['Gender'].value_counts()
```




    Male      329
    Other     316
    Female    303
    Name: Gender, dtype: int64



Vaikuttaa siltä, että jokaista sukupuolta on datasetissä noin kolmasosa. Tässä tapauksessa voisimme siis arpoa sukupuolen, jokaisen sukupuolen todennäköisyyden ollessa 0.3:


```python
df['Gender']=df['Gender'].fillna(np.random.choice(['Female', 'Male', 'Other'], p=[1/3, 1/3, 1/3]))
```

Varmistetaan vielä, ettei datasetti sisällä enää puuttuvia arvoja:


```python
df.isna().sum()
```




    Student_id    0
    First_name    0
    Last_name     0
    Points        0
    Enrolled      0
    Age           0
    Gender        0
    dtype: int64



Tässä datasetissä sukupuoli on kategorinen muuttuja. Koska useimmat koneoppimisalgoritmit haluavat vain numeerisia arvoja, kategoriset muuttujat on hyvä muuttaa numeeriksi. 

Tätä varten muutetaan eri luokat omiksi sarakkeiksi, ja merkitään 0 tai 1 merkiksi siitä, kuuluuko rivin opiskelija tiettyyn luokkaan.


```python
df=pd.get_dummies(df, columns=['Gender'])
```



Nyt Gender-sarakkeen arvot on muutettu numeerisiksi, voimme tarkistaa tämän ottamalla 5 ensimmäistä riviä:


```python
df.head()
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
      <th>Gender_Female</th>
      <th>Gender_Male</th>
      <th>Gender_Other</th>
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
      <td>1</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>10001</td>
      <td>Emily</td>
      <td>Atkins</td>
      <td>17</td>
      <td>1</td>
      <td>30.0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>2</th>
      <td>10002</td>
      <td>Sanna</td>
      <td>Atkins</td>
      <td>291</td>
      <td>1</td>
      <td>32.0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>10003</td>
      <td>Outi</td>
      <td>Sanchez</td>
      <td>273</td>
      <td>1</td>
      <td>35.0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>10004</td>
      <td>Dina</td>
      <td>Smith</td>
      <td>273</td>
      <td>0</td>
      <td>34.0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
    </tr>
  </tbody>
</table>
</div>



Lisäksi voimme vielä karsia turhat sarakkeet. Jos ajatellaan, että haluaisimme muodostaa koneoppimismallin, jonka tavoitteena on ennustaa, ilmottautuuko opiskelija läsnäolevaksi, haluamme ottaa kyseisen sarakkeen omaan DataFrameen ja poistaa se nykyisestä. Yleensä puhutaan feature ja target-dataframeista:


```python
df_target=df['Enrolled']
df_features=df.drop('Enrolled', axis=1)
```

Mitä muita sarakkeita uskaltaisimme poistaa?
Poistamisessa tarvitsee yleensä olla todella tarkkana, ja eri muuttujien merkitsevyyden mittaamiseksi on erilaisia menetelmiä. Tässä tapauksessa menemme kuitenkin mutulla.

Nimet ovat yleensä hyviä ehdokkaita poistettavaksi, jos ne eivät ole kategorisia muuttujia tai jos ne ovat, niillä on usein myös numeerinen vastine. Esimerkiksi vaaleissa yhdellä äänestysrivillä voisi olla tieto siitä, kenelle ääni meni, mutta todennäköisempää on, että rivillä on tieto ehdokkaan numerosta. Tässä tapauksessa kyse ei ole kuitenkaan siitä, joten poistetaan etu- ja sukunimi -sarakkeet.


```python
df_features=df_features.drop(['First_name', 'Last_name'], axis=1)
```

Myös erilaiset rivikohtaiset tunnisteet voidaan yleensä poistaa. Tässä tapauksessa siis opiskelijatunnus.


```python
df_features=df_features.drop('Student_id', axis=1)
```

Katsotaan nyt, miltä datasetti näyttää.


```python
df_features.head(20)
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
      <th>Points</th>
      <th>Age</th>
      <th>Gender_Female</th>
      <th>Gender_Male</th>
      <th>Gender_Other</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>265</td>
      <td>35.000000</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>17</td>
      <td>30.000000</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>2</th>
      <td>291</td>
      <td>32.000000</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>273</td>
      <td>35.000000</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>273</td>
      <td>34.000000</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>5</th>
      <td>245</td>
      <td>35.000000</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>6</th>
      <td>230</td>
      <td>33.381303</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>7</th>
      <td>285</td>
      <td>28.000000</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>8</th>
      <td>215</td>
      <td>25.000000</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>9</th>
      <td>241</td>
      <td>38.000000</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>10</th>
      <td>153</td>
      <td>43.000000</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>11</th>
      <td>234</td>
      <td>38.000000</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>12</th>
      <td>145</td>
      <td>37.000000</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <th>13</th>
      <td>177</td>
      <td>31.000000</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <th>14</th>
      <td>300</td>
      <td>33.000000</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <th>15</th>
      <td>204</td>
      <td>37.000000</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>16</th>
      <td>226</td>
      <td>34.000000</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <th>17</th>
      <td>162</td>
      <td>23.000000</td>
      <td>0</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <th>18</th>
      <td>51</td>
      <td>37.000000</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>19</th>
      <td>152</td>
      <td>33.381303</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
    </tr>
  </tbody>
</table>
</div>



Mukana on siis enää ikä, opintopisteiden määrä ja sukupuoli. Kaikki ne ovat numeerisissa muodossa, joten teoriassa tämän perusteella voitaisiin muodostaa malli koneoppimisen avulla.

Tähän teoriaosuuteen liittyy jo aiemmin ladatun tehtävän ([jos et ladannut sitä vielä, voit tehdä sen tästä]({{ OSlevelUPkoodarit.github.io }}{% link /notebooks/Python_exercise.ipynb %})) osio 2.

Esimerkkivastaus tehtäviin löytyy ([tästä]({{ OSlevelUPkoodarit.github.io }}{% link /notebooks/python_example_solution.ipynb %})).




