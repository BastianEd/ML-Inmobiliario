# Predicción del precio de viviendas en Ames, Iowa

Proyecto de Machine Learning para estimar el precio de venta de viviendas a partir de variables físicas, constructivas y de ubicación del dataset Ames Housing.

El trabajo incluye limpieza y análisis exploratorio, detección de valores atípicos, segmentación no supervisada, comparación de modelos supervisados, optimización de hiperparámetros, ensambles y evaluación en validación cruzada y conjunto de prueba.

## Objetivo

Construir un modelo de regresión que estime `SalePrice` con el menor error posible y seleccionar la solución óptima mediante métricas comparables y una validación que limite la fuga de datos.

### Métricas principales

- **MAE:** error absoluto medio en dólares; métrica principal de decisión.
- **RMSE:** penaliza con mayor intensidad los errores de predicción grandes.
- **R²:** proporción de la variación del precio explicada por el modelo.

## Contenido del proyecto

- `EDA_final.ipynb`: notebook principal con el análisis completo.
- `Ames_Iowa_Housing_Dataset.csv`: dataset de 2.930 viviendas y 82 variables.
- `requirements.txt`: dependencias de Python.


## Metodología

### 1. Limpieza y análisis exploratorio

- Diagnóstico de valores duplicados y faltantes.
- Eliminación de tres propiedades atípicas con superficies superiores a 4.000 pies cuadrados y precios no representativos.
- Relleno de variables categóricas y numéricas dentro de los pipelines de modelado.
- Análisis de correlaciones y visualizaciones de distribución y relaciones con `SalePrice`.

### 2. Segmentación no supervisada

Se utiliza clustering para identificar perfiles de propiedades y examinar diferencias comerciales entre segmentos. El análisis emplea `K = 4` y considera las características preparadas dentro del notebook.

### 3. Modelado supervisado

Se comparan modelos de regresión base y optimizados, incluyendo enfoques lineales y basados en árboles. La preparación del dato se realiza mediante `Pipeline` y `ColumnTransformer` para evitar fugas de información.

### 4. Optimización y ensambles

- Validación cruzada de 5 folds con los mismos folds para las comparaciones.
- Búsqueda aleatoria de hiperparámetros usando MAE como métrica de negocio.
- Implementación de `VotingRegressor` y `StackingRegressor`.
- Confirmación final en un conjunto de prueba reservado.

## Resultados principales

Los principales impulsores del precio son la calidad general, la superficie habitable, el área total del sótano, la capacidad del garaje y el año de construcción.

En la comparación documentada en el notebook, el modelo de ensamble **Stacking** obtuvo:

- MAE en conjunto de prueba: **11.364,488 USD**
- RMSE en conjunto de prueba: **16.499,833 USD**
- R² en conjunto de prueba: **0,966**
- MAE en validación cruzada: **12.840,568 USD**

Las cifras corresponden a la ejecución de referencia con semilla `42`. Los resultados exactos pueden variar según el entorno, las versiones de las librerías y la capacidad de ejecución.

## Instalación

Se recomienda utilizar un entorno virtual de Python.

```bash
python -m venv .venv
```

Activar el entorno en Windows:

```bash
.venv\Scripts\activate
```

Instalar las dependencias:

```bash
pip install -r requirements.txt
```

## Ejecución

Abrir el proyecto en Jupyter o VS Code y ejecutar todas las celdas de:

```text
EDA_final.ipynb
```

También puede iniciar Jupyter desde la terminal:

```bash
jupyter notebook
```

La ejecución completa puede tardar aproximadamente 15 minutos debido a las búsquedas de hiperparámetros y al modelo Stacking.

## Dependencias

- NumPy
- Pandas
- Matplotlib
- Seaborn
- scikit-learn
- SciPy

## Consideraciones

- Los datos provienen del mercado inmobiliario de Ames, Iowa, por lo que la generalización a otras ciudades requiere validación adicional.
- Las variables geográficas pueden reflejar diferencias históricas y sesgos presentes en el mercado.
- El modelo debe usarse como apoyo a la tasación profesional y no como sustituto de una inspección inmobiliaria.
- Para una puesta en producción se recomienda implementar monitorización de deriva, auditoría de sesgos y revisión periódica del modelo.
