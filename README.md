# 📝 **Caso**
>***Una discográfica busca lanzar un nuevo artista y utiliza datos de Spotify para analizar el éxito de las canciones en 2023. Se plantean hipótesis sobre la relación entre BPM, popularidad en otras plataformas, presencia en playlists, número de canciones del artista y características de la canción con el número de streams. El objetivo es validar estas hipótesis y proporcionar recomendaciones estratégicas para aumentar las posibilidades de éxito del artista.***

#### Se realizara un análisis para validar o refutar las siguientes hipótesis:

-Las canciones con un mayor BPM (Beats Por Minuto) tienen más éxito en términos de cantidad de streams en Spotify.

-Las canciones más populares en el ranking de Spotify también tienen un comportamiento similar en otras plataformas como Deezer.

-La presencia de una canción en un mayor número de playlists se relaciona con un mayor número de streams.

-Los artistas con un mayor número de canciones en Spotify tienen más streams.

-Las características de la música influyen en el éxito en términos de cantidad de streams en Spotify.


![Banner Inicio](https://github.com/jesolav/Validaci-n-Hip-tesis_Proyecto-2/assets/172732181/477b6121-2b2c-4161-9746-c69fd11e7ed8)


### 🤜🤛 Equipo: Camila Maluenda - Jenifer Soto

## ⚙️ Herramientas y Recursos
- Bigquery / SQL
- Python
- Google Slides
- Power BI

### 📄Conjunto de datos
El dataset contiene datos sobre las canciones más reproducidas en Spotify en 2023. Los datos se dividen en 3 tablas, la primera sobre el rendimiento de cada canción en Spotify, la segunda con el rendimiento en otras plataformas como Deezer o Apple Music, y la tercera con las características de estas canciones.

#### **Trackinspotify**

-track_id: Identificador único de la canción. Es un número entero de 7 dígitos que no se repite

-track_name: Nombre de la canción

-artist(s)_name: Nombre del artista(s) de la canción

-artist_count: Número de artistas que contribuyen a la canción.

-released_year: Año en que se lanzó la canción.

-released_month: Mes en el que se lanzó la canción.

-released_day: Día del mes en que se lanzó la canción.

-inspotifyplaylists: Número de listas de reproducción de Spotify en las que está incluida la canción

-inspotifycharts: Presencia y ranking de la canción en las listas de Spotify

-streams: Número total de transmisiones en Spotify. Representa la cantidad de veces que la canción fue escuchada.

#### **Trackincompetition**

-track_id: Identificador único de la canción. Es un número entero de 7 dígitos que no se repite

-inappleplaylists: número de listas de reproducción de Apple Music en las que está incluida la canción

-inapplecharts: Presencia y rango de la canción en las listas de Apple Music

-indeezerplaylists: Número de listas de reproducción de Deezer en las que está incluida la canción

-indeezercharts: Presencia y rango de la canción en las listas de Deezer

-inshazamcharts: Presencia y rango de la canción en las listas de Shazam


#### **Tracktechnicalinfo**

-track_id: Identificador único de la canción. Es un número entero de 7 dígitos que no se repite

-bpm: Pulsaciones por minuto, una medida del tiempo de la canción.

-key: Clave musical de la canción

-mode: Modo de la canción (mayor o menor)

-danceability_%: Porcentaje que indica qué tan adecuada es la canción para bailar

-valence_: Positividad del contenido musical de la canción.

-energy_: Nivel de energía percibido de la canción.

-acusticness_: Cantidad de sonido acústico en la canción.

-instrumentality_: Cantidad de contenido instrumental en la canción.

-liveness_: Presencia de elementos de actuación en vivo.

-speechiness_: Cantidad de palabras habladas en la canción.

### 💻 [Procesamiento y preparación para analisis de datos:](https://github.com/jesolav/Validaci-n-Hip-tesis_Proyecto-2/tree/8b49998a8745a5f15fb7156893002e8308d5197f/1.%20Procesar%20y%20preparar%20base%20de%20datos).

1. [Importación y Creación de Tablas en BigQuery:](https://github.com/jesolav/Validacion_Hipotesis_Proyecto_2_Laboratoria/blob/9b18f8a6d510e875659ca2f3772b59410602e5c3/1.%20Procesar%20y%20preparar%20base%20de%20datos/1.%20Conectar%20importar%20datos%20a%20otras%20herramientas.md)
2. [Identificación y Manejo de Valores Nulos:](https://github.com/jesolav/Validaci-n-Hip-tesis_Proyecto-2/blob/8b49998a8745a5f15fb7156893002e8308d5197f/1.%20Procesar%20y%20preparar%20base%20de%20datos/2.%20Identificar%20y%20manejar%20valores%20nulos.md)
3. [Manejo de Valores Duplicados:](https://github.com/jesolav/Validaci-n-Hip-tesis_Proyecto-2/blob/8b49998a8745a5f15fb7156893002e8308d5197f/1.%20Procesar%20y%20preparar%20base%20de%20datos/3.%20Manejo%20Duplicados.md)
4. [Identificar y manejar datos fuera del alcance del análisis:](https://github.com/jesolav/Validaci-n-Hip-tesis_Proyecto-2/blob/8b49998a8745a5f15fb7156893002e8308d5197f/1.%20Procesar%20y%20preparar%20base%20de%20datos/4.%20Identificar%20y%20manejar%20datos%20fuera%20del%20alcance%20del%20analisis.md)
5. [Identificación y Manejo de Datos Discrepantes en variables categóricas:](https://github.com/jesolav/Validaci-n-Hip-tesis_Proyecto-2/blob/8b49998a8745a5f15fb7156893002e8308d5197f/1.%20Procesar%20y%20preparar%20base%20de%20datos/5.%20Identificacion%20y%20Manejo%20de%20Datos%20Discrepantes%20en%20variables%20categoricas.md)
6. [Identificación y Manejo de Datos Discrepantes en variables numéricas:](https://github.com/jesolav/Validaci-n-Hip-tesis_Proyecto-2/blob/8b49998a8745a5f15fb7156893002e8308d5197f/1.%20Procesar%20y%20preparar%20base%20de%20datos/6.%20Identificacion%20y%20Manejo%20de%20Datos%20Discrepantes%20en%20Variables%20Numericas.md)
7. [Comprobar y cambiar tipo de dato:](https://github.com/jesolav/Validaci-n-Hip-tesis_Proyecto-2/blob/8b49998a8745a5f15fb7156893002e8308d5197f/1.%20Procesar%20y%20preparar%20base%20de%20datos/7.%20Comprobar%20y%20cambiar%20tipo%20de%20dato.md)
8. [Crear nuevas variables:](https://github.com/jesolav/Validaci-n-Hip-tesis_Proyecto-2/blob/8b49998a8745a5f15fb7156893002e8308d5197f/1.%20Procesar%20y%20preparar%20base%20de%20datos/8.%20Crear%20nuevas%20variables.md)
9. [Unir Tablas:](https://github.com/jesolav/Validaci-n-Hip-tesis_Proyecto-2/blob/8b49998a8745a5f15fb7156893002e8308d5197f/1.%20Procesar%20y%20preparar%20base%20de%20datos/9.%20Unir%20Tablas.md)
10. [Construir tablas auxiliares:](https://github.com/jesolav/Validaci-n-Hip-tesis_Proyecto-2/blob/8b49998a8745a5f15fb7156893002e8308d5197f/1.%20Procesar%20y%20preparar%20base%20de%20datos/10.%20Construir%20tablas%20auxiliares.md)


---------------------------------------------------------------------------------------------------------------------------------------------------------------------------

### 🔎[Análisis Exploratorio en Power Bi:](https://github.com/jesolav/Validaci-n-Hip-tesis_Proyecto-2/tree/c7893cc200d8e0ee01b9d5c5544266f23a79e4be/2.%20Analisis%20Exploratorio)

1. [Agrupar datos según variables categóricas:](https://github.com/jesolav/Validacion_Hipotesis_Proyecto_2_Laboratoria/blob/501156e0312f89fd7f435c83293669fe4884e2f8/2.%20Analisis%20Exploratorio/1.%20Agrupar%20datos%20segun%20variables%20categoricas.md)

2. [Visualizar las variables categóricas:](https://github.com/jesolav/Validaci-n-Hip-tesis_Proyecto-2/blob/4bddd705f73a0c8db6236dc3598a2f7144ead456/2.%20Analisis%20Exploratorio/2.%20Visualizar%20las%20variables%20categoricas.md)

3. [Aplicar medidas de tendencia central:](https://github.com/jesolav/Validaci-n-Hip-tesis_Proyecto-2/blob/4bddd705f73a0c8db6236dc3598a2f7144ead456/2.%20Analisis%20Exploratorio/3.%20Medidas%20Tendencia%20Central%2C%20Histograma.md)

4. [Visualizar distribución en histograma:](https://github.com/jesolav/Validacion_Hipotesis_Proyecto_2_Laboratoria/blob/9ab7ab7c1dd68b969a40d8f9f29e793a642e9a04/2.%20Analisis%20Exploratorio/4.%20Visualizar%20Distribucion.md)

5. [Aplicar medidas de dispersión:](https://github.com/jesolav/Validaci-n-Hip-tesis_Proyecto-2/blob/4bddd705f73a0c8db6236dc3598a2f7144ead456/2.%20Analisis%20Exploratorio/5.%20Medidas%20Tendencia%20Central%2C%20Histograma.md)

6. [Visualizar el comportamiento de los datos a lo largo del tiempo:](https://github.com/jesolav/Validaci-n-Hip-tesis_Proyecto-2/blob/c80b496a15a0bc34e6e087dfd2af3231192d1d94/2.%20Analisis%20Exploratorio/6.%20Comportamiento%20en%20el%20tiempo.md)

7. [Calcular cuartiles, deciles o percentiles:](https://github.com/jesolav/Validaci-n-Hip-tesis_Proyecto-2/blob/4bddd705f73a0c8db6236dc3598a2f7144ead456/2.%20Analisis%20Exploratorio/7.%20Calcular%20cuartiles%2C%20deciles%20o%20percentiles.md)

8. [Calcular correlación entre variables](https://github.com/jesolav/Validaci-n-Hip-tesis_Proyecto-2/blob/4bddd705f73a0c8db6236dc3598a2f7144ead456/2.%20Analisis%20Exploratorio/8.%20Calcular%20correlacion%20entre%20variables.md)

---------------------------------------------------------------------------------------------------------------------------------------------------------------------------

### 📈[Aplicar técnica de análisis:](https://github.com/jesolav/Validaci-n-Hip-tesis_Proyecto-2/tree/4bddd705f73a0c8db6236dc3598a2f7144ead456/3.%20Aplicar%20t%C3%A9cnica%20de%20analisis)

1. [Aplicar segmentación](https://github.com/jesolav/Validaci-n-Hip-tesis_Proyecto-2/blob/4bddd705f73a0c8db6236dc3598a2f7144ead456/3.%20Aplicar%20t%C3%A9cnica%20de%20analisis/1.%20Aplicar%20segmentaci%C3%B3n.md)
2. [Validar Hipótesis:](https://github.com/jesolav/Validaci-n-Hip-tesis_Proyecto-2/tree/4bddd705f73a0c8db6236dc3598a2f7144ead456/3.%20Aplicar%20t%C3%A9cnica%20de%20analisis/2.%20Validar%20Hipotesis)

   ▫️ [Hipótesis 1](https://github.com/jesolav/Validaci-n-Hip-tesis_Proyecto-2/blob/4bddd705f73a0c8db6236dc3598a2f7144ead456/3.%20Aplicar%20t%C3%A9cnica%20de%20analisis/2.%20Validar%20Hipotesis/Hipotesis%201.md)

   ▫️ [Hipótesis 2](https://github.com/jesolav/Validaci-n-Hip-tesis_Proyecto-2/blob/4bddd705f73a0c8db6236dc3598a2f7144ead456/3.%20Aplicar%20t%C3%A9cnica%20de%20analisis/2.%20Validar%20Hipotesis/Hipotesis%202.md)

   ▫️ [Hipótesis 3](https://github.com/jesolav/Validaci-n-Hip-tesis_Proyecto-2/blob/4bddd705f73a0c8db6236dc3598a2f7144ead456/3.%20Aplicar%20t%C3%A9cnica%20de%20analisis/2.%20Validar%20Hipotesis/Hipotesis%203.md)

   ▫️ [Hipótesis 4](https://github.com/jesolav/Validaci-n-Hip-tesis_Proyecto-2/blob/4bddd705f73a0c8db6236dc3598a2f7144ead456/3.%20Aplicar%20t%C3%A9cnica%20de%20analisis/2.%20Validar%20Hipotesis/Hipotesis%204.md)

   ▫️ [Hipótesis 5](https://github.com/jesolav/Validaci-n-Hip-tesis_Proyecto-2/blob/4bddd705f73a0c8db6236dc3598a2f7144ead456/3.%20Aplicar%20t%C3%A9cnica%20de%20analisis/2.%20Validar%20Hipotesis/Hipotesis%205.md)


### 💡 Dashboard
[Imagen](https://github.com/jesolav/Validaci-n-Hip-tesis_Proyecto-2/blob/b3cb28c4dbe7f099fe7eb7c714929595bfc9b9fa/Dashboard/Dashboard.png)

[Archivo PowerBi](https://drive.google.com/file/d/1NXnE4NTZZPbcXGLEPu638dMgAjgVbxHQ/view?usp=sharing)


### 📰 [Presentación](https://drive.google.com/file/d/1OXI_-uZVE-AB3Sb9WxEq271WotgcIo4S/view?usp=sharing)

### 🧩 [Conclusiones y Recomendaciones](https://github.com/jesolav/Validacion_Hipotesis_Proyecto_2_Laboratoria/blob/501156e0312f89fd7f435c83293669fe4884e2f8/Conclusiones%20y%20Recomendaciones/Conclusiones.md)

