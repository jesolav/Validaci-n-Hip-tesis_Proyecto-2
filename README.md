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

2. [Identificación y Manejo de Valores Nulos:](https://github.com/jesolav/Nulos_hipotesis.git)


3. [Manejo de Valores Duplicados:](https://github.com/jesolav/duplicados_hipotesis.git)


4. Identificar y manejar datos fuera del alcance del análisis

Al analizar nuestras tablas, decidimos eliminar columnas irrelevantes (key, mode) en track_technical_info, dado que no son relevantes para el análisis.

_Consulta utilizada:_
```sql
CCREATE OR REPLACE TABLE `proyecto-hipotesis-426418.hipotesis.track_technical` AS
SELECT
  * EXCEPT (key, mode)
FROM
  `proyecto-hipotesis-426418.hipotesis.track_technical`;
```

5. Identificación y Manejo de Datos Discrepantes en variables categóricas:

_Consulta utilizada:_
```sql
CREATE OR REPLACE TABLE `proyecto-hipotesis-427018.hipotesis.track_in_spotify` AS
SELECT
  track_id,
  REGEXP_REPLACE(track_name, r'[^a-zA-Z0-9\s]', '') AS track_name,
  REGEXP_REPLACE(artist_s__name, r'[^a-zA-Z0-9\s]', '') AS artist_s__name,
  artist_count,
  released_year,
  released_month,
  released_day,
  in_spotify_playlists,
  in_spotify_charts,
  streams
FROM
  `proyecto-hipotesis-427018.hipotesis.track_in_spotify`
```
Esta consulta reemplaza  la tabla track_in_spotify en la que los nombres de las canciones (track_name) y los nombres de los artistas (artists_name) se han limpiado, eliminando todos los caracteres especiales, dejando solo letras, números y espacios. Se incluyen todas las columnas originales de la tabla track_in_spotify.

6. Identificación y Manejo de Datos Discrepantes en variables numéricas:

6.1 Tabla track_technical

Al verificar que las columnas relevantes ya están en el tipo de dato INTEGER, podemos proceder directamente con los cálculos.

_Consulta utilizada:_
```sql
CREATE TABLE `proyecto-hipotesis-427018.hipotesis.estadisticas_track_technical` AS (
  SELECT
    'bpm' AS Variable,
    MAX(bpm) AS Valor_Maximo,
    MIN(bpm) AS Valor_Minimo,
    ROUND(AVG(bpm), 2) AS Valor_Promedio
  FROM
    `proyecto-hipotesis-427018.hipotesis.track_technical`
  UNION ALL
  SELECT
    'danceability_%' AS Variable,
    MAX(`danceability_%`) AS Valor_Maximo,
    MIN(`danceability_%`) AS Valor_Minimo,
    ROUND(AVG(`danceability_%`), 2) AS Valor_Promedio
  FROM
    `proyecto-hipotesis-427018.hipotesis.track_technical`
  UNION ALL
  SELECT
    'valence_%' AS Variable,
    MAX(`valence_%`) AS Valor_Maximo,
    MIN(`valence_%`) AS Valor_Minimo,
    ROUND(AVG(`valence_%`), 2) AS Valor_Promedio
  FROM
    `proyecto-hipotesis-427018.hipotesis.track_technical`
  UNION ALL
  SELECT
    'energy_%' AS Variable,
    MAX(`energy_%`) AS Valor_Maximo,
    MIN(`energy_%`) AS Valor_Minimo,
    ROUND(AVG(`energy_%`), 2) AS Valor_Promedio
  FROM
    `proyecto-hipotesis-427018.hipotesis.track_technical`
  UNION ALL
  SELECT
    'acousticness_%' AS Variable,
    MAX(`acousticness_%`) AS Valor_Maximo,
    MIN(`acousticness_%`) AS Valor_Minimo,
    ROUND(AVG(`acousticness_%`), 2) AS Valor_Promedio
  FROM
    `proyecto-hipotesis-427018.hipotesis.track_technical`
  UNION ALL
  SELECT
    'instrumentalness_%' AS Variable,
    MAX(`instrumentalness_%`) AS Valor_Maximo,
    MIN(`instrumentalness_%`) AS Valor_Minimo,
    ROUND(AVG(`instrumentalness_%`), 2) AS Valor_Promedio
  FROM
    `proyecto-hipotesis-427018.hipotesis.track_technical`
  UNION ALL
  SELECT
    'liveness_%' AS Variable,
    MAX(`liveness_%`) AS Valor_Maximo,
    MIN(`liveness_%`) AS Valor_Minimo,
    ROUND(AVG(`liveness_%`), 2) AS Valor_Promedio
  FROM
    `proyecto-hipotesis-427018.hipotesis.track_technical`
  UNION ALL
  SELECT
    'speechiness_%' AS Variable,
    MAX(`speechiness_%`) AS Valor_Maximo,
    MIN(`speechiness_%`) AS Valor_Minimo,
    ROUND(AVG(`speechiness_%`), 2) AS Valor_Promedio
  FROM
    `proyecto-hipotesis-427018.hipotesis.track_technical`);
```
![image](https://github.com/jesolav/Validaci-n-Hip-tesis_Proyecto-2/assets/172732181/8c20da0d-50c5-4ddb-b706-1bd130e3fefa)

6.2 Tabla track_in_competition

Verificamos que las columnas in_apple_playlists, in_apple_charts, in_deezer_playlists, in_deezer_charts e in_shazam_charts ya son de tipo INTEGER, son adecuadas para nuestros cálculos.

_Consulta utilizada:_
```sql
CREATE TABLE `proyecto-hipotesis-427017.hipotesis.estadisticas_track_in_competition` AS (
  SELECT
    'in_apple_playlists' AS Variable,
    MAX(in_apple_playlists) AS Valor_Maximo,
    MIN(in_apple_playlists) AS Valor_Minimo,
    ROUND(AVG(in_apple_playlists), 2) AS Valor_Promedio
  FROM
    `proyecto-hipotesis-427017.hipotesis.track_in_competition`
  UNION ALL
  SELECT
    'in_apple_charts' AS Variable,
    MAX(in_apple_charts) AS Valor_Maximo,
    MIN(in_apple_charts) AS Valor_Minimo,
    ROUND(AVG(in_apple_charts), 2) AS Valor_Promedio
  FROM
    `proyecto-hipotesis-427017.hipotesis.track_in_competition`
  UNION ALL
  SELECT
    'in_deezer_playlists' AS Variable,
    MAX(in_deezer_playlists) AS Valor_Maximo,
    MIN(in_deezer_playlists) AS Valor_Minimo,
    ROUND(AVG(in_deezer_playlists), 2) AS Valor_Promedio
  FROM
    `proyecto-hipotesis-427017.hipotesis.track_in_competition`
  UNION ALL
  SELECT
    'in_deezer_charts' AS Variable,
    MAX(in_deezer_charts) AS Valor_Maximo,
    MIN(in_deezer_charts) AS Valor_Minimo,
    ROUND(AVG(in_deezer_charts), 2) AS Valor_Promedio
  FROM
    `proyecto-hipotesis-427017.hipotesis.track_in_competition`
  UNION ALL
  SELECT
    'in_shazam_charts' AS Variable,
    MAX(in_shazam_charts) AS Valor_Maximo,
    MIN(in_shazam_charts) AS Valor_Minimo,
    ROUND(AVG(in_shazam_charts), 2) AS Valor_Promedio
  FROM
    `proyecto-hipotesis-427017.hipotesis.track_in_competition`);
```
Esta consulta crea una nueva tabla estadisticas_track_in_competition para identificar los valores máximo, mínimo y promedio de track_in_competition por cada una de las variables.

![image](https://github.com/jesolav/Validaci-n-Hip-tesis_Proyecto-2/assets/172732181/606a1eaf-f5b6-46b0-8607-8405feafd09a)

6.3 Tabla track_in_spotify 

Esta tabla cuenta con una columna streams con valores no numéricos, por lo que se procede a:
-Limpieza de datos: Se eliminan los caracteres no numéricos y se reemplazan las cadenas vacías con nulos en las columnas relevantes.
-Conversión a enteros: Los valores limpios se convierten a enteros de 64 bits.
-Cálculo de estadísticas: Se calculan el valor máximo, mínimo y promedio para cada columna.
-Combinación de resultados: Los resultados de las tres subconsultas se combinan en una sola tabla utilizando UNION ALL.
-Creación de tabla: Se crea la tabla estadisticas_track_in_spotify con los resultados combinados.

_Consulta utilizada:_
```sql
CREATE TABLE `proyecto-hipotesis-427017.hipotesis.estadisticas_track_in_spotify` AS (SELECT
 'in_spotify_playlists' AS Variable,
 MAX(in_spotify_playlists) AS Valor_Maximo,
 MIN(in_spotify_playlists) AS Valor_Minimo,
 ROUND(AVG(in_spotify_playlists), 2) AS Promedio
FROM
 `proyecto-hipotesis-427017.hipotesis.track_in_spotify`
UNION ALL
SELECT
 'in_spotify_charts' AS Variable,
 MAX(in_spotify_charts) AS Valor_Maximo,
 MIN(in_spotify_charts) AS Valor_Minimo,
 ROUND(AVG(in_spotify_charts), 2) AS Promedio
FROM
 `proyecto-hipotesis-427017.hipotesis.track_in_spotify`
UNION ALL
SELECT
 'streams' AS Variable,
 MAX(SAFE_CAST(streams AS INT64)) AS Valor_Maximo,
 MIN(SAFE_CAST(streams AS INT64)) AS Valor_Minimo,
 ROUND(AVG(SAFE_CAST(streams AS FLOAT64)), 2) AS Promedio
FROM
 `proyecto-hipotesis-427017.hipotesis.track_in_spotify`
WHERE
 SAFE_CAST(streams AS INT64) IS NOT NULL)
```

![image](https://github.com/jesolav/Validaci-n-Hip-tesis_Proyecto-2/assets/172732181/3103a1aa-abb8-4c87-ac62-64dab54c3013)

La consulta genera una tabla con estadísticas básicas (máximo, mínimo y promedio) para tres variables de interés (in_spotify_playlists, in_spotify_charts, y streams) en la tabla track_in_spotify. Utiliza la unión (UNION ALL) para combinar los resultados de cada variable en una única salida y emplea SAFE_CAST para manejar de forma segura la conversión de la variable streams a tipo numérico.


7. Comprobar y cambiar tipo de dato
se ejecutó una consulta para identificar los valores en la columna streams que no podían ser convertidos a números, asegurando que todos los valores fueran numéricos.

_Consulta utilizada:_
```sql
SELECT DISTINCT streams
FROM `proyecto-hipotesis-427018.hipotesis.track_in_spotify`
WHERE SAFE_CAST(streams AS INT64) IS NULL;
```
Se identifica valor no numérico en columna streams:
'BPM110KeyAModeMajorDanceability53Valence75Energy69Acousticness7Instrumentalness0Liveness17Speechiness3'

8. Crear nuevas variables
8.1_track_in_spotify_release_date

En la hoja “track_in_spotify Utilizando las columnas released_year, released_month y released_day, combinamos estas columnas en una nueva columna release_date con el formato aaaa-mm-dd.
_Consulta utilizada:_
```sql
CREATE OR REPLACE TABLE `proyecto-hipotesis-427017.hipotesis.track_in_spotify` AS
SELECT
  track_id,
  track_name,
  artist_s__name AS artists_name,
  artist_count,
  released_year,
  released_month,
  released_day,
  in_spotify_playlists,
  in_spotify_charts,
  streams,
  CAST(CONCAT(CAST(released_year AS STRING), '-', 
              LPAD(CAST(released_month AS STRING), 2, '0'), '-', 
              LPAD(CAST(released_day AS STRING), 2, '0')) AS DATE) AS release_date
FROM
  `proyecto-hipotesis-427017.hipotesis.track_in_spotify`;
```

8.2 track_in_competition_nueva_columna

_Consulta utilizada:_
```sql
CREATE OR REPLACE TABLE `proyecto-hipotesis-427017.hipotesis.track_in_competition_updated` AS
SELECT
  c.track_id,
  c.in_apple_playlists,
  c.in_apple_charts,
  c.in_deezer_playlists,
  c.in_deezer_charts,
  c.in_shazam_charts,
  s.total_playlists
FROM
  `proyecto-hipotesis-427017.hipotesis.track_in_competition` c
LEFT JOIN
  `proyecto-hipotesis-427017.hipotesis.track_in_spotify_total_playlists` s
ON
  c.track_id = s.track_id;
```

8.3 Columna Categoria Artista: Solo o Feat en tabla unificada

_Consulta utilizada:_
```sql
CREATE OR REPLACE TABLE `proyecto-hipotesis-427017.hipotesis.tabla_matriz` AS
WITH solo_artists AS (
  SELECT
    artists_name,
    COUNT(track_id) AS total_canciones
  FROM
    `proyecto-hipotesis-427017.hipotesis.tabla_unificada`
  WHERE
    artist_count = 1
  GROUP BY
    artists_name
)
SELECT
  a.*,
  CASE
    WHEN solo_artists.artists_name IS NOT NULL THEN 'solo'
    ELSE 'feat'
  END AS artist_category
FROM
  `proyecto-hipotesis-427017.hipotesis.tabla_matriz` a
LEFT JOIN
  solo_artists
ON
  a.artists_name = solo_artists.artists_name;
  ```

8.4 Columna Cuartiles para streams en tabla_matriz

_Consulta utilizada:_
```sql
CREATE OR REPLACE TABLE `proyecto-hipotesis-427017.hipotesis.tabla_matriz` AS
WITH Quartiles AS (
  SELECT
    streams,
    NTILE(4) OVER (ORDER BY streams) AS quartile_streams
  FROM
    `proyecto-hipotesis-427017.hipotesis.tabla_matriz`
)
SELECT
  a.*,
  Quartiles.quartile_streams,
  CASE
    WHEN Quartiles.quartile_streams = 1 THEN 'Bajo'
    WHEN Quartiles.quartile_streams = 2 THEN 'Medio-Bajo'
    WHEN Quartiles.quartile_streams = 3 THEN 'Medio-Alto'
    WHEN Quartiles.quartile_streams = 4 THEN 'Alto'
  END AS categoria_streams
FROM
  `proyecto-hipotesis-427017.hipotesis.tabla_matriz` a
LEFT JOIN Quartiles
ON a.streams = Quartiles.streams
```

9. Unir Tablas

Durante el proceso de unir tablas en BigQuery, surgió un error debido a que las columnas track_id tenían tipos de datos diferentes (INTEGER en una tabla y STRING en otra). Este tipo de incompatibilidad impide la comparación y unión directa de columnas.
Solución
Para resolver este problema, se convirtió el tipo de dato de la columna track_id de INTEGER a STRING en todas las tablas antes de realizar la unión. Esto se hizo utilizando la función CAST en SQL, que permite cambiar el tipo de dato de una columna.

_Consulta utilizada:_
```sql
CREATE OR REPLACE TABLE `proyecto-hipotesis-427017.hipotesis.tabla_unificada` AS
SELECT
  s.track_id,
  s.track_name,
  s.artists_name,
  s.artist_count,
  s.released_year,
  s.released_month,
  s.released_day,
  s.in_spotify_playlists,
  s.in_spotify_charts,
  s.streams,
  s.release_date,
  c.in_apple_playlists,
  c.in_apple_charts,
  c.in_deezer_playlists,
  c.in_deezer_charts,
  c.in_shazam_charts,
  c.total_playlists AS total_playlists,
  t.bpm,
  t.`danceability_%`,
  t.`valence_%`,
  t.`energy_%`,
  t.`acousticness_%`,
  t.`instrumentalness_%`,
  t.`liveness_%`,
  t.`speechiness_%`
FROM
  `proyecto-hipotesis-427017.hipotesis.track_in_spotify` s
LEFT JOIN
  `proyecto-hipotesis-427017.hipotesis.track_in_competition_updated` c
ON
  s.track_id = c.track_id
LEFT JOIN
  `proyecto-hipotesis-427017.hipotesis.track_technical` t
ON
  s.track_id = t.track_id;
```


10. Construir tablas auxiliares

WITH solo_artists AS (...): Define una tabla temporal llamada solo_artists que selecciona el nombre del artista y cuenta el número de canciones (track_id) donde artist_count es igual a 1.
SELECT artists_name, COUNT(track_id) AS total_canciones: Selecciona el nombre del artista y cuenta el número de canciones.
FROM ...: Especifica la tabla tabla_unificada como la fuente de datos.
WHERE artist_count = 1: Filtra las filas donde artist_count es igual a 1, indicando que el artista es solista.
GROUP BY artists_name: Agrupa los resultados por el nombre del artista.
SELECT * FROM solo_artists;: Selecciona todos los datos de la tabla temporal solo_artists para crear la tabla final total_canciones_solo_artists.

_Consulta utilizada:_
```sql
CREATE OR REPLACE TABLE `proyecto-hipotesis-427017.hipotesis.total_canciones_solo_artists` AS
WITH solo_artists AS (
 SELECT
   artists_name,
   COUNT(track_id) AS total_canciones
 FROM
   `proyecto-hipotesis-427017.hipotesis.tabla_unificada`
 WHERE
   artist_count = 1
 GROUP BY
   artists_name
)
SELECT
 *
FROM
 solo_artists;
```

---------------------------------------------------------------------------------------------------------------------------------------------------------------------------

### 🔎 Análisis Exploratorio en power bi

1. Agrupar datos según variables categóricas
   ![image](https://github.com/jesolav/Validaci-n-Hip-tesis_Proyecto-2/assets/172732181/40e9239b-a2e2-4856-8fd8-bc63bbcf8d12)

2. Visualizar las variables categóricas
   ![image](https://github.com/jesolav/Validaci-n-Hip-tesis_Proyecto-2/assets/172732181/40fb2f6e-bb2a-4957-b2d8-68870910c066)

3. Aplicar medidas de tendencia central
4. Visualizar distribución en histograma
5. Aplicar medidas de dispersión	

 ![image](https://github.com/jesolav/Validaci-n-Hip-tesis_Proyecto-2/assets/172732181/e952f2b4-a46b-4d93-aca3-69653f83939f)

6. Visualizar el comportamiento de los datos a lo largo del tiempo
   ![image](https://github.com/jesolav/Validaci-n-Hip-tesis_Proyecto-2/assets/172732181/37a2dbd7-8650-4a5a-83bb-9caa7aab0060)

7. Calcular cuartiles, deciles o percentiles	
Se utilizaron consultas en big query para cada caracteristica para dividir en cuartiles. Dejando el cuartil 1-2 como bajo, y 3-4 como alto.

```sql
CREATE OR REPLACE TABLE `proyecto-hipotesis-427017.hipotesis.tabla_acousticness` AS
WITH Quartiles AS (
  SELECT
    track_id,
    nombre variable,
    streams,
    NTILE(4) OVER (ORDER BY acousticness_percentage / 100) AS cuartil
  FROM
    `proyecto-hipotesis-427017.hipotesis.tabla_matriz`
),
categorias AS (
  SELECT
    nombre variable,
    streams,
    cuartil,
    CASE
      WHEN cuartil IN (1, 2) THEN 'bajo'
      WHEN cuartil IN (3, 4) THEN 'alto'
    END AS categoria
  FROM
    Quartiles
)
SELECT
  categoria,
  AVG(streams) AS promedio_streams
FROM
  categorias
GROUP BY
  categoria
ORDER BY
  categoria;
```

![image](https://github.com/jesolav/Validaci-n-Hip-tesis_Proyecto-2/assets/172732181/b1cfc1a8-508d-4b57-bed3-41a9a5843b43)





