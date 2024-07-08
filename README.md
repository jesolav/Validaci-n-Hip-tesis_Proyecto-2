# 📝 **Caso**
>***Una discográfica busca lanzar un nuevo artista y utiliza datos de Spotify para analizar el éxito de las canciones en 2023. Se plantean hipótesis sobre la relación entre BPM, popularidad en otras plataformas, presencia en playlists, número de canciones del artista y características de la canción con el número de streams. El objetivo es validar estas hipótesis y proporcionar recomendaciones estratégicas para aumentar las posibilidades de éxito del artista.***

#### Se realizara un análisis para validar o refutar las siguientes hipótesis:

-Las canciones con un mayor BPM (Beats Por Minuto) tienen más éxito en términos de cantidad de streams en Spotify.
-Las canciones más populares en el ranking de Spotify también tienen un comportamiento similar en otras plataformas como Deezer.
-La presencia de una canción en un mayor número de playlists se relaciona con un mayor número de streams.
-Los artistas con un mayor número de canciones en Spotify tienen más streams.
-Las características de la música influyen en el éxito en términos de cantidad de streams en Spotify.
-Las el modo de la canción "Minor" o "Major" influye en la cantidad de reproducciones de la misma.

![Banner Inicio](https://github.com/jesolav/Validaci-n-Hip-tesis_Proyecto-2/assets/172732181/477b6121-2b2c-4161-9746-c69fd11e7ed8)


### 🤜🤛 Equipo: Camila Maluenda - Jenifer Soto

## ⚙️ Herramientas y Recursos
- Bigquery
- SQL
- Python
- Google Slides
- Power BI

### 📄Conjunto de datos
-
-

### 🔎 Procesamiento y preparación para anlisis de datos

1. Importación y Creación de Tablas en BigQuery:
      Proyecto: proyecto-hipotesis
      Tablas importadas: track_in_competition, track_in_spotify, track_technical_info

2.Identificación y Manejo de Valores Nulos:
    track_in_competition: 50 nulos en in_shazam_charts

    
    track_technical_info: 95 nulos en key
Consultas SQL utilizadas para contar valores nulos en cada columna de las tablas.
Manejo de Valores Duplicados:
Identificación de duplicados principalmente en track_in_spotify.
Consultas SQL para contar valores duplicados en cada tabla.
Eliminación de Valores Fuera del Alcance del Análisis:
Eliminación de columnas irrelevantes (key, mode) en track_technical_info.
Consultas SQL para excluir columnas.
Identificación y Manejo de Datos Discrepantes:
Manejo de símbolos en track_in_spotify mediante expresiones regulares.
Identificación de discrepancias en valores numéricos utilizando funciones MAX, MIN y AVG.
Cambio de Tipos de Datos:
Conversión de streams de STRING a INTEGER en track_in_spotify.
Consultas SQL para realizar los cambios de tipo de datos.
Creación de Nuevas Variables:
Creación de la variable release_date en track_in_spotify.
Consultas SQL para concatenar y formatear fechas.
Unión de Tablas:
Limpieza y creación de vistas con datos limpios para cada tabla.
Unión de las tablas limpias (track_in_spotify, track_in_competition, track_technical_info) mediante LEFT JOIN.
Construcción de Tablas Auxiliares:
Uso de tablas temporales para analizar el total de canciones por artista y la participación en playlists.
Consultas SQL con la estructura WITH para crear estas tablas auxiliares.

