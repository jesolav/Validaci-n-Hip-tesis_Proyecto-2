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


Consulta en sql:

