# 7. Calcular cuartiles, deciles o percentiles

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


![image](https://github.com/jesolav/Nulos_hipotesis/assets/172732181/4d51c38c-5ec3-4f9e-a5a6-3a4c149959c1)


La imagen muestra la suma de los promedios de streams de canciones clasificadas en categorías "alto" y "bajo" para diferentes características musicales. A partir de estos datos, podemos analizar la relación entre estas características y el éxito musical, medido por el promedio de streams.

## Análisis por característica:

-**Instrumentalness (Instrumentalidad)**: Las canciones con bajo contenido instrumental (mayor presencia de voces) tienen un promedio de streams considerablemente mayor que aquellas con alto contenido instrumental. Esto sugiere que las canciones con letras y voces tienden a ser más populares y exitosas en términos de reproducciones.

-**Energy (Energía)**: Las canciones con alta energía tienen un promedio de streams ligeramente superior a las de baja energía. Esto indica que las canciones más enérgicas y animadas pueden ser más atractivas para los oyentes y generar más reproducciones.

-**Valence (Valencia)**: Las canciones con valencia alta (más positivas y alegres) tienen un promedio de streams similar a las de valencia baja (más negativas y tristes). Esto sugiere que la valencia no es un factor determinante en el éxito de una canción en términos de reproducciones.

-**Acousticness (Acústica)**: Las canciones con baja acústica (menos instrumentos acústicos) tienen un promedio de streams ligeramente superior a las de alta acústica. Esto podría indicar que las canciones con sonidos más modernos y electrónicos pueden ser más populares en plataformas de streaming.

-**Liveness (Sonido en vivo)**: Las canciones con bajo sonido en vivo (grabadas en estudio) tienen un promedio de streams ligeramente superior a las de alto sonido en vivo. Esto sugiere que la mayoría de los oyentes prefieren canciones con una producción de estudio más pulida.

-**Danceability (Bailabilidad)**: Las canciones con baja bailabilidad tienen un promedio de streams ligeramente superior a las de alta bailabilidad. Esto podría indicar que, en general, las canciones menos bailables son más populares en plataformas de streaming, aunque la diferencia no es muy significativa.

-**Speechiness (Presencia de voz hablada)**: Las canciones con baja presencia de voz hablada tienen un promedio de streams considerablemente mayor que aquellas con alta presencia de voz hablada. Esto sugiere que las canciones con predominio de canto son más populares y exitosas en términos de reproducciones.


## Relación con el éxito musical:

En general, podemos observar que las características que parecen tener una mayor influencia en el éxito musical (medido por el promedio de streams) son la instrumentalidad, la presencia de voz hablada y, en menor medida, la energía y la acústica. 
Las canciones con bajo contenido instrumental, baja presencia de voz hablada, alta energía y baja acústica tienden a tener un mayor número de reproducciones.

Sin embargo, es importante tener en cuenta que estas son tendencias generales y que existen muchos otros factores que pueden influir en el éxito de una canción, como la calidad de la composición, la promoción y marketing, y la conexión con el público. Además, las preferencias de los oyentes pueden variar según el género musical y otros factores individuales.
