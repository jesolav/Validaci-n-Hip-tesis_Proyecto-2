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
