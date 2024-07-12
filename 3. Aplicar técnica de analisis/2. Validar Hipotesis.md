# 2. Validar hipótesis

## *Hipótesis 1: Las canciones con un mayor BPM (Beats por minuto) tienen más éxito en términos de streams en Spotify*

*Coeficiente correlación bpm y streams:*

![image](https://github.com/user-attachments/assets/d7f2c3b9-c5db-4e03-be2b-f58b8e0f46a4)

Consulta en sql:
```sql 
SELECT
 CORR(BPM, streams) AS correlation_value
FROM
 `proyecto-hipotesis-427018.hipotesis.tabla_matriz`
```

El valor sugiere una correlación negativa muy débil entre los BPM de una canción y la cantidad de streams. En otras palabras, parece que no hay una relación significativa entre el ritmo de una canción y su éxito en términos de streams. 

*Lo graficamos en power bi con python*

```phyton
# El código siguiente, que crea un dataframe y quita las filas duplicadas, siempre se ejecuta y actúa como un preámbulo del script:
# dataset = pandas.DataFrame(total_playlists, streams)
# dataset = dataset.drop_duplicates()
# Pegue o escriba aquí el código de script:
import matplotlib.pyplot as plt
# Los datos son cargados automáticamente por Power BI en el dataframe 'dataset'
# Crear el gráfico de dispersión
plt.figure(figsize=(10, 6))
plt.scatter(dataset['bpm'], dataset['streams'], alpha=0.5)
plt.title('Relación entre bpm y Streams')
plt.xlabel('bpm')
plt.ylabel('Streams')
plt.grid(True)
plt.show()
```


![image](https://github.com/user-attachments/assets/34645e3a-c1ef-405c-b98c-0defa53554ad)


El gráfico de dispersión muestra la relación entre el BPM (Beats por minuto) de una canción y su número de reproducciones (streams) en Spotify. Cada punto en el gráfico representa una canción, con su posición en el eje x indicando su BPM y su posición en el eje y indicando su número de reproducciones.

**Análisis del gráfico:**

* **No hay una relación clara:** Los puntos están dispersos por todo el gráfico, sin un patrón evidente que sugiera una relación lineal entre el BPM y las reproducciones. Esto significa que canciones con BPM alto y bajo pueden tener tanto un número alto como bajo de reproducciones.
  
* **Mayor densidad en BPM bajos:** Hay una mayor concentración de canciones con BPM entre 80 y 120, lo que indica que este rango de tempo es más común en el conjunto de datos. Sin embargo, esto no significa que las canciones en este rango tengan necesariamente más reproducciones.

**Correlación:**

La correlación de -0.0023 confirma lo que se observa en el gráfico: prácticamente no hay relación lineal entre el BPM y las reproducciones. Un valor tan cercano a cero indica que el BPM no es un factor determinante en el éxito de una canción en términos de reproducciones en Spotify.

**Conclusión:**

Basándonos en este gráfico y en el valor de correlación, podemos rechazar la hipótesis 1: "Las canciones con un mayor BPM (Beats por minuto) tienen más éxito en términos de streams en Spotify". Los datos no respaldan esta afirmación, ya que no se observa una relación significativa entre el BPM y el número de reproducciones.


------------------------------------------------------------------------------------------------------

## *Hipótesis 2: Las canciones más populares en el ranking de Spotify también tienen un comportamiento similar en otras plataformas como Deezer*

*Coeficiente correlación deezer_charts y spotify_charts:*

![image](https://github.com/user-attachments/assets/3dc4e8bb-fc33-4495-9da4-f55b4f178a19)

Consulta en sql:
```sql 
SELECT CORR(in_spotify_charts, in_deezer_charts) AS correlation_value
FROM `proyecto-hipotesis-427017.hipotesis.tabla_matriz`
```

El coeficiente de correlación de 0.6048 confirma la relación positiva observada en el gráfico. Este valor indica una correlación moderadamente fuerte, lo que sugiere que la popularidad en Spotify es un predictor razonablemente bueno de la popularidad en Deezer, y viceversa.

*Lo graficamos en power bi con python*

```phyton
import matplotlib.pyplot as plt
import numpy as np

# Personalización de colores y estilo
fig, ax = plt.subplots(figsize=(10, 6), facecolor='#000000')
ax.set_facecolor('#896FF780')

# Cálculo de la línea de tendencia
z = np.polyfit(dataset['in_spotify_charts'], dataset['in_deezer_charts'], 1)
p = np.poly1d(z)

# Gráfico de dispersión
plt.scatter(dataset['in_spotify_charts'], dataset['in_deezer_charts'], alpha=0.5, color='#9071CE')

# Línea de tendencia
plt.plot(dataset['in_spotify_charts'], p(dataset['in_spotify_charts']), linestyle='--', color='white')

# Configuración de textos y etiquetas
plt.title('Relación entre Popularidad en Spotify y Deezer en 2023', fontsize=18, color='white', fontname='Calibri')
plt.xlabel('Rank en Spotify', color='white', fontname='Calibri')
plt.ylabel('Rank en Deezer', color='white', fontname='Calibri')

# Configuración de ejes y cuadrícula
plt.xlim([dataset['in_spotify_charts'].min(), dataset['in_spotify_charts'].max()])
plt.ylim([dataset['in_deezer_charts'].min(), dataset['in_deezer_charts'].max()])
plt.xticks(color='white', fontname='Calibri')
plt.yticks(color='white', fontname='Calibri')
plt.grid(True, alpha=0.3)

# Mostrar el gráfico
plt.show()
```

![image](https://github.com/user-attachments/assets/13d5fedc-b49e-4b5f-bde4-1d4ed16a5ed0)

El gráfico de dispersión muestra la relación entre el ranking de popularidad de canciones en Spotify y Deezer en 2023. Cada punto representa una canción, con su posición en el eje x indicando su ranking en Spotify y su posición en el eje y indicando su ranking en Deezer.

**Análisis del gráfico:**

* **Tendencia Positiva:** Los puntos en el gráfico muestran una clara tendencia ascendente, lo que indica que a medida que aumenta el ranking en Spotify (es decir, a medida que una canción es menos popular en Spotify), también tiende a aumentar el ranking en Deezer. Esto sugiere una relación positiva entre la popularidad en ambas plataformas.
* **Dispersión:** Aunque hay una tendencia general, también hay una dispersión considerable de los puntos alrededor de la línea de tendencia. Esto significa que si bien hay una relación positiva, no es perfecta y hay excepciones. Algunas canciones pueden ser más populares en una plataforma que en la otra.

**Conclusión:**

Basándonos en el gráfico de dispersión y el coeficiente de correlación, podemos afirmar que existe una relación positiva moderadamente fuerte entre la popularidad en Spotify y Deezer en 2023. Esto significa que las canciones que son populares en una plataforma tienden a serlo también en la otra, aunque hay excepciones y la relación no es perfecta.

**Limitaciones:**

Es importante tener en cuenta que este análisis se basa en un conjunto de datos específico y solo se refiere a la popularidad en 2023. La relación entre las plataformas podría variar en otros años o con diferentes conjuntos de datos. Además, la correlación no implica causalidad, por lo que no podemos concluir que la popularidad en una plataforma cause directamente la popularidad en la otra. Podrían existir otros factores que influyan en la popularidad en ambas plataformas.


----------------------------------------------------

## *Hipótesis 3: La presencia de una canción en un mayor número de playlists se relaciona con un mayor número de streams*

*Coeficiente correlación total playlists y streams:*

![image](https://github.com/user-attachments/assets/23325d7f-228d-463e-9856-45d2b08ad7af)

Consulta en sql:
```sql 
SELECT CORR(total_playlists, streams) AS correlation_value
FROM `proyecto-hipotesis-427018.hipotesis.tabla_matriz`
```

El coeficiente de correlación de 0.6047 confirma la relación positiva observada en el gráfico. Este valor indica una correlación moderadamente fuerte, lo que sugiere que la presencia en playlists es un predictor razonablemente bueno del número de streams, pero no el único factor determinante.

*Lo graficamos en power bi con python*

```phyton
import matplotlib.pyplot as plt
import numpy as np

# Personalización de colores y estilo
fig, ax = plt.subplots(figsize=(10, 6), facecolor='#000000')
ax.set_facecolor('#896FF780')

# Cálculo de la línea de tendencia
z = np.polyfit(dataset['total_playlists'], dataset['streams'], 1)
p = np.poly1d(z)

# Gráfico de dispersión
plt.scatter(dataset['total_playlists'], dataset['streams'], alpha=0.5, color='#9071CE')

# Línea de tendencia
plt.plot(dataset['total_playlists'], p(dataset['total_playlists']), linestyle='--', color='white')

# Configuración de textos y etiquetas
plt.title('Relación entre Popularidad en Total Playlists y Streams', fontsize=18, color='white', fontname='Calibri')
plt.xlabel('total_playlists', color='white', fontname='Calibri')
plt.ylabel('Streams', color='white', fontname='Calibri')

# Configuración de ejes y cuadrícula
plt.xlim([dataset['total_playlists'].min(), dataset['total_playlists'].max()])
plt.ylim([dataset['streams'].min(), dataset['streams'].max()])
plt.xticks(color='white', fontname='Calibri')
plt.yticks(color='white', fontname='Calibri')
plt.grid(True, alpha=0.3)

# Mostrar el gráfico
plt.show()
```

![image](https://github.com/user-attachments/assets/dd394b0f-f5db-4867-9073-fba651deb79e)



**Análisis del gráfico:**

* **Tendencia positiva**: El gráfico de dispersión muestra una clara tendencia ascendente, lo que indica que a medida que aumenta el número de playlists en las que aparece una canción, también tiende a aumentar su número de streams.
* **Dispersión**: Aunque hay una tendencia general, también hay una dispersión considerable de los puntos alrededor de la línea de tendencia. Esto significa que si bien hay una relación positiva, no es perfecta y hay excepciones. Algunas canciones pueden tener muchos streams sin estar en muchas playlists, y viceversa.

**Conclusión:**

Basándonos en el gráfico y el coeficiente de correlación, podemos concluir que la tercera hipótesis es válida: existe una relación positiva moderadamente fuerte entre la presencia de una canción en playlists y su número de streams. Esto significa que las canciones que aparecen en más playlists tienden a tener más streams, aunque hay excepciones y otros factores también influyen en la popularidad de una canción.


------------------------------------------------------------------------------------------------------

## *Hipótesis 4: Los artistas con un mayor número de canciones en Spotify tienen más streams*

*Coeficiente correlación total canciones por artista y streams:*

![image](https://github.com/user-attachments/assets/830d8b83-7f64-4485-8eb5-980da7154af3)

Consulta en sql:
```sql
WITH song_count AS (
  SELECT
    artists_name,
    COUNT(track_id) AS total_songs
  FROM
    `proyecto-hipotesis-427017.hipotesis.tabla_matriz`
  GROUP BY
    artists_name
),


-- Crear una tabla temporal para sumar los streams por artista
stream_sum AS (
  SELECT
    artists_name,
    SUM(streams) AS total_streams
  FROM
    `proyecto-hipotesis-427017.hipotesis.tabla_matriz`
  GROUP BY
    artists_name
),


-- Unir los resultados de las dos tablas temporales
artist_data AS (
  SELECT
    song_count.artists_name,
    song_count.total_songs,
    stream_sum.total_streams
  FROM
    song_count
  JOIN
    stream_sum
  ON
    song_count.artists_name = stream_sum.artists_name
)


-- Calcular la correlación entre el número de canciones y los streams totales
SELECT
  CORR(total_songs, total_streams) AS correlation_value
FROM
  artist_data
```

El coeficiente de correlación de 0.7789 confirma la fuerte relación positiva observada en la tabla y el gráfico. Este valor indica una correlación fuerte, lo que significa que el número de canciones de un artista es un buen predictor de su número de reproducciones en Spotify.

*Lo graficamos en power bi con python*

```phyton
import matplotlib.pyplot as plt
import numpy as np

# Personalización de colores y estilo
fig, ax = plt.subplots(figsize=(10, 6), facecolor='#000000')
ax.set_facecolor('#896FF780')

# Cálculo de la línea de tendencia
z = np.polyfit(dataset['in_spotify_playlists'], dataset['streams'], 1)
p = np.poly1d(z)

# Gráfico de dispersión
plt.scatter(dataset['in_spotify_playlists'], dataset['streams'], alpha=0.5, color='#9071CE')

# Línea de tendencia
plt.plot(dataset['in_spotify_playlists'], p(dataset['in_spotify_playlists']), linestyle='--', color='white')

# Configuración de textos y etiquetas
plt.title('Relación entre Popularidad en Playlists Spotify y Streams', fontsize=18, color='white', fontname='Calibri')
plt.xlabel('in_spotify_playlists', color='white', fontname='Calibri')
plt.ylabel('Streams', color='white', fontname='Calibri')

# Configuración de ejes y cuadrícula
plt.xlim([dataset['in_spotify_playlists'].min(), dataset['in_spotify_playlists'].max()])
plt.ylim([dataset['streams'].min(), dataset['streams'].max()])
plt.xticks(color='white', fontname='Calibri')
plt.yticks(color='white', fontname='Calibri')
plt.grid(True, alpha=0.3)

# Mostrar el gráfico
plt.show()
```
![image](https://github.com/user-attachments/assets/9f4319c2-00d4-400b-8a29-89a4c845d8f8)

**Análisis del gráfico:**

* **Tendencia positiva clara**: El gráfico de dispersión muestra una fuerte tendencia ascendente, lo que indica que a medida que aumenta el número de canciones de un artista en Spotify, también aumenta su número de reproducciones.
* **Pocos valores atípicos**: Aunque hay cierta dispersión, la mayoría de los puntos se agrupan alrededor de la línea de tendencia, lo que sugiere que la relación es bastante consistente en todos los artistas.

**Conclusión:**

Basándonos en el análisis de la tabla, el gráfico y el coeficiente de correlación, podemos afirmar que la cuarta hipótesis es válida: existe una fuerte relación positiva entre el número de canciones de un artista en Spotify y la cantidad de reproducciones que recibe. Esto sugiere que los artistas con más canciones disponibles tienden a tener más éxito en términos de reproducciones en la plataforma.


------------------------------------------------------------------------------------------------------

## *Hipótesis 5: Las características de la canción influyen en el éxito en términos de streams en Spotify*

*Coeficiente correlación deezer_charts y spotify_charts:*

![image](https://github.com/user-attachments/assets/a582295c-81ca-4b7d-8d97-1eb7b5d7b68b)

Consulta en sql:
```sql
SELECT
 CORR(danceability_percentage, streams) AS danceability_corr,
 CORR(valence_percentage, streams) AS valence_corr,
 CORR(energy_percentage, streams) AS energy_corr,
 CORR(acousticness_percentage, streams) AS acousticness_corr,
 CORR(instrumentalness_percentage, streams) AS instrumentalness_corr,
 CORR(liveness_percentage, streams) AS liveness_corr,
 CORR(speechiness_percentage, streams) AS speechiness_corr
FROM
 `proyecto-hipotesis-427017.hipotesis.tabla_matriz`;
```

Todos los coeficientes son cercanos a cero, lo que indica una correlación muy débil o nula entre cada característica y el número de streams.

* **Correlaciones negativas débiles:** Danceability, energy, valence, instrumentalness, liveness y speechiness tienen correlaciones negativas débiles con los streams. Esto sugiere una ligera tendencia a que las canciones con valores más altos en estas características tengan menos streams, pero la relación es muy débil.
* **Correlación casi nula:** La correlación entre acousticness y streams es prácticamente nula, lo que indica que no hay relación entre esta característica y el número de reproducciones.

*Lo graficamos en power bi con python*

```phyton
import matplotlib.pyplot as plt
import numpy as np

# Lista de características a analizar
features = [
    'danceability_percentage', 'valence_percentage', 'energy_percentage',
    'acousticness_percentage', 'instrumentalness_percentage', 'liveness_percentage',
    'speechiness_percentage'
]

# Colores y estilo personalizado (tomados del primer gráfico)
colores = {
    'fondo_figura': '#000000',
    'fondo_ejes': '#896FF780', 
    'puntos': '#9071CE',
    'linea_tendencia': 'white',
    'texto': 'white'
}

# Configuración de la figura
plt.figure(figsize=(15, 15), facecolor=colores['fondo_figura'])  # Fondo de la figura

# Gráficos individuales
for i, feature in enumerate(features):
    ax = plt.subplot(4, 2, i + 1, facecolor=colores['fondo_ejes'])  # Fondo de los ejes

    # Scatter plot con personalización
    plt.scatter(dataset[feature], dataset['streams'], alpha=0.5, color=colores['puntos'], edgecolors='black')

    # Línea de tendencia
    z = np.polyfit(dataset[feature], dataset['streams'], 1)
    p = np.poly1d(z)
    plt.plot(dataset[feature], p(dataset[feature]), linestyle='--', color=colores['linea_tendencia'])

    # Configuración de textos, etiquetas y ejes
    plt.title(f'Relación entre {feature} y Streams', fontsize=14, color=colores['texto'], fontname='Calibri')
    plt.xlabel(feature, color=colores['texto'], fontname='Calibri')
    plt.ylabel('Streams', color=colores['texto'], fontname='Calibri')
    plt.xticks(color=colores['texto'], fontname='Calibri')
    plt.yticks(color=colores['texto'], fontname='Calibri')
    ax.spines['bottom'].set_color(colores['texto'])  # Color de los bordes de los ejes
    ax.spines['top'].set_color(colores['texto'])
    ax.spines['right'].set_color(colores['texto'])
    ax.spines['left'].set_color(colores['texto'])
    ax.tick_params(axis='x', colors=colores['texto'])  # Color de las marcas de los ejes
    ax.tick_params(axis='y', colors=colores['texto'])
    plt.grid(True, alpha=0.3) 

# Ajustar el diseño para evitar superposiciones
plt.tight_layout()
plt.show()
```

![image](https://github.com/user-attachments/assets/d5dc0839-69a6-49e8-968d-6ecbad3a289d)


**Conclusión:**

Basándonos en los gráficos y los coeficientes de correlación, no podemos confirmar la Hipótesis 5. Los datos no muestran una influencia significativa de las características de las canciones en el éxito en términos de streams en Spotify. Es probable que otros factores, como la popularidad del artista, el género musical, la promoción y el marketing, tengan un impacto más significativo en el número de reproducciones.

**Conclusión:**

* **Limitaciones del análisis:** Este análisis se basa en un conjunto de datos específico y en correlaciones lineales. Es posible que existan relaciones no lineales o interacciones entre las características que no se hayan considerado.
Posibles explicaciones: La falta de correlación podría deberse a que las preferencias de los oyentes son muy diversas y no se pueden explicar únicamente por las características musicales de las canciones.
* **Investigación adicional:** Sería interesante explorar otros factores que podrían influir en el éxito de las canciones en Spotify, como los mencionados anteriormente (popularidad del artista, género musical, promoción, etc.).
