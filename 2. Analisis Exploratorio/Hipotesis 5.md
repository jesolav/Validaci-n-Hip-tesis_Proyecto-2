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
