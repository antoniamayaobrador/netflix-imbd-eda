# Análisis y Predicción de Contenidos en Netflix

## Introducción

La plataforma de contenidos audiovisuales **Netflix** es un agente imprescindible en el panorama de consumo audiovisual contemporáneo. Por ello, realizar un análisis de los contenidos de la plataforma resulta interesante para derivar insights culturales. Además, un paso más allá es modelar los datos para obtener predicciones sobre las notas de productos audiovisuales.

## Dataset

El análisis se ha basado en el dataset de Kaggle [Netflix IMDB Scores](https://www.kaggle.com/datasets/thedevastator/netflix-imdb-scores/data).

Este dataset incluye información sobre los títulos disponibles en Netflix, tales como:
- Título
- Año de lanzamiento
- Certificación por edades
- Duración
- Puntuación en IMDb
- Número de votos

### Enriquecimiento del Dataset
Antes de empezar a trabajar con los datos:
- **Información adicional generada con ChatGPT:** Se procesaron los títulos en batches de 400 películas para obtener datos adicionales como géneros, país, continente y lenguaje.
- **Código relacionado:** El proceso completo para enriquecer el dataset está documentado en el archivo `Netflixpre.ipynb`.

## Análisis Realizado

El análisis incluye las siguientes etapas:

1. **Visualizaciones generales** y ajuste de incongruencias en los datos.
2. Relaciones entre películas y series por países.
3. Evolución temporal del runtime en diferentes categorías.
4. Identificación de outliers en runtime por tipo, género y país.
5. Distribución de las puntuaciones en IMDb, tanto generales como por tipo de producto.
6. Estudio de outliers y valores más altos en IMDb scores.
7. Consideraciones sobre la columna `age_certification`: valores nulos y disponibles.
8. Análisis de la relación entre países, géneros y su puntuación media en IMDb mediante mapas de calor.
9. **Tests estadísticos** para verificar los análisis previos y extraer conclusiones.

## Conclusiones del Análisis

Aunque el notebook incluye muchos más insights detallados, algunas conclusiones destacadas son:

- **Diversidad cultural en los contenidos:** 
  - En países como India se producen contenidos en más de 5 idiomas, lo que refleja la complejidad cultural y estratégica de cada mercado nacional.
  
- **Distribución de series y películas por países:**
  - Corea del Sur tiene un 72.4% de series frente a India, donde este porcentaje es menor al 10%.

- **Formatos híbridos:**
  - Series cortas con capítulos largos y películas de menor duración (como documentales o cómicas) están difuminando las fronteras tradicionales entre películas y series.

- **Fenómenos de fandom y hate en IMDb:**
  - Las puntuaciones medias están concentradas entre 6 y 8. Sin embargo, ciertos productos generan reacciones extremas, como campañas de desprestigio hacia un cómico brasileño infantil o altas puntuaciones para documentales y anime por efecto de fans.

- **Auge de la animación:**
  - La animación, especialmente asiática, muestra un crecimiento considerable en Netflix.

## Sistema de Predicción de Valoración

### Desafíos Iniciales
- La baja cantidad de datos en las valoraciones de 0 a 3.5-4 dificultó la predicción de malas valoraciones.
- Se probaron técnicas como **oversampling**, que no resolvieron el problema de sesgo hacia puntuaciones medias.

### Modelo Final
- Se optó por una combinación de varios modelos **XGBoost** por tramos de notas con:
  - **Validación cruzada**
  - **Búsqueda de hiperparámetros**
  - Tramos de valoraciones específicas para ajustar las predicciones.
- El modelo final combinó las predicciones con un **Random Forest Regressor** y un sesgo dinámico negativo para corregir la sobreestimación.

### Resultados
- El **RMSE final** obtenido fue de **0.5285**, lo que permite un error de medio punto al predecir una valoración de película.

---

Para más detalles, consulta los notebooks adjuntos en este repositorio.
