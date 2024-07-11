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

### 🔎 Procesamiento y preparación para analisis de datos 
. [Procesamiento y preparación para analisis de datos:](https://github.com/jesolav/Validaci-n-Hip-tesis_Proyecto-2/tree/6060b18be30d2ed3037561ba14222757aa3b241a/Procesamiento%20y%20preparci%C3%B3n%20para%20anlisis%20de%20datos
)


1. Importación y Creación de Tablas en BigQuery:
      Proyecto: proyecto-hipotesis
      Tablas importadas: track_in_competition, track_in_spotify, track_technical_info

2. [Identificación y Manejo de Valores Nulos:](https://github.com/jesolav/Nulos_hipotesis.git)
2. [Identificación y Manejo de Valores Nulos:](https://github.com/jesolav/Validaci-n-Hip-tesis_Proyecto-2/blob/main/1.%20Procesar%20y%20preparar%20base%20de%20datos/2.%20Identificar%20y%20manejar%20valores%20nulos.md)

3. [Manejo de Valores Duplicados:](https://github.com/jesolav/duplicados_hipotesis.git)

4. [Identificar y manejar datos fuera del alcance del análisis:](https://github.com/jesolav/datos-fuera-del-alcance_hipotesis.git)

5. [Identificación y Manejo de Datos Discrepantes en variables categóricas:](https://github.com/jesolav/Identificaci-n-y-Manejo-de-Datos-Discrepantes-en-variables-categ-ricas_hipotesis.git)

6. [Identificación y Manejo de Datos Discrepantes en variables numéricas:](https://github.com/jesolav/Identificaci-n-y-Manejo-de-Datos-Discrepantes-en-variables-num-ricas_hipotesis.git)


7. [Comprobar y cambiar tipo de dato:](https://github.com/jesolav/-Comprobar-y-cambiar-tipo-de-dato_hipotesis.git)

8. [Crear nuevas variables:](https://github.com/jesolav/Crear-nuevas-variables_hipotesis.git)

9. [Unir Tablas:](https://github.com/jesolav/Crear-nuevas-variables_hipotesis.git)

10. [Construir tablas auxiliares:](https://github.com/jesolav/Construir-tablas-auxiliares_hipotesis.git)


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





