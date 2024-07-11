# 2. Identificación y Manejo de Valores Nulos:

Se realizan consultas para identificar nulos, y se decide mantener dado que no afectan en el análisis.

-*track_in_spotify : sin nulos*

-*track_in_competition: 50 nulos*

_Consulta utilizada:_

```sql
SELECT
  COUNTIF(track_id IS NULL) AS null_track_id,
  COUNTIF(in_apple_playlists IS NULL) AS null_in_apple_playlists,
  COUNTIF(in_apple_charts IS NULL) AS null_in_apple_charts,
  COUNTIF(in_deezer_playlists IS NULL) AS null_in_deezer_playlists,
  COUNTIF(in_deezer_charts IS NULL) AS null_in_deezer_charts,
  COUNTIF(in_shazam_charts IS NULL) AS null_in_shazam_charts
FROM `proyecto-hipotesis-427017.hipotesis.track_in_competition`;
```

-*track_technical_info: 95 nulos en key*

_Consulta utilizada:_
```sql
SELECT
    COUNTIF(track_id IS NULL) AS null_track_id,
    COUNTIF(bpm IS NULL) AS null_bpm,
    COUNTIF(key IS NULL) AS null_key,
    COUNTIF(mode IS NULL) AS null_mode,
    COUNTIF(`danceability_%` IS NULL) AS null_danceability,
    COUNTIF(`valence_%` IS NULL) AS null_valence,
    COUNTIF(`energy_%` IS NULL) AS null_energy,
    COUNTIF(`acousticness_%` IS NULL) AS null_acousticness,
    COUNTIF(`instrumentalness_%` IS NULL) AS null_instrumentalness,
    COUNTIF(`liveness_%` IS NULL) AS null_liveness,
    COUNTIF(`speechiness_%` IS NULL) AS null_speechiness
FROM `proyecto-hipotesis-427017.hipotesis.track_technical`;
```
