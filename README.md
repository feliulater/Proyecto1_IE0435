# Proyecto 1 - IE0435

## Clasificación de contaminaciones en una línea de producción simulada

Este repositorio contiene el desarrollo del Proyecto 1 del curso **IE0435 - Inteligencia Artificial Aplicada a la Ingeniería Eléctrica**. El objetivo del proyecto es construir un sistema de clasificación capaz de detectar la presencia de granos de arroz como contaminaciones en una línea de producción simulada, utilizando técnicas de aprendizaje automático clásico.

## Descripción del proyecto

La simulación se realizó utilizando imágenes tomadas sobre una hoja blanca. Las imágenes con presencia de granos de arroz se clasifican como muestras positivas, mientras que las imágenes sin arroz o con otros objetos se clasifican como muestras negativas.

Cada imagen fue procesada para convertirla en una representación numérica. Para esto, las imágenes fueron transformadas a escala de grises, redimensionadas a **128x128 píxeles**, binarizadas y convertidas en vectores fila. Cada vector contiene **16384 valores de píxeles** y una columna final correspondiente a la etiqueta de clasificación.

La codificación utilizada fue:

- `1`: fondo blanco.
- `0`: presencia de objeto.
- Etiqueta `1`: imagen con arroz.
- Etiqueta `0`: imagen sin arroz.

## Estructura del repositorio

```text
Proyecto1_IE0435/
│
├── data/
│   ├── personal/
│   │   └── matriz_final.csv
│   │
│   ├── group_inputs/
│   │   ├── dataset1.csv
│   │   ├── dataset2.csv
│   │   ├── dataset4.csv
│   │   └── dataset5.csv
│   │
│   └── processed/
│       └── dataset_grupo_final.csv
│
├── models/
│   └── mejor_modelo.joblib
│
├── reports/
│   └── resultados_modelos.png
│
├── src/
│   ├── proyecto_arroz.py
│   ├── conjunto_datos.py
│   └── eval_modelos.py
│
├── DATASET.md
├── MODEL_CARD.md
├── README.md
├── requirements.txt
└── LICENSE
```

## Scripts utilizados

### `src/proyecto_arroz.py`

Este script se encarga de convertir las imágenes originales en matrices binarias. Lee imágenes desde las carpetas `Positivo` y `Negativo`, las convierte a escala de grises, las redimensiona a **128x128 píxeles**, aplica binarización mediante el método de Otsu y genera un archivo CSV con los datos vectorizados.

### `src/conjunto_datos.py`

Este script une los archivos CSV individuales del grupo. Valida que cada archivo tenga el formato correcto, es decir, **16385 columnas** correspondientes a 16384 píxeles más una etiqueta final. Además, verifica que los valores sean únicamente `0` y `1`.

### `src/eval_modelos.py`

Este script entrena y evalúa distintos modelos clásicos de clasificación. El conjunto de datos se divide en una proporción **80% entrenamiento** y **20% prueba**. Luego se comparan diferentes algoritmos y se exporta el mejor modelo en formato `.joblib`.

## Modelos evaluados

Los modelos evaluados fueron:

| Modelo | Accuracy |
|---|---:|
| SVM Lineal | 0.5667 |
| SVM RBF | 0.5333 |
| KNN k=3 | 0.6000 |
| KNN k=5 | 0.5667 |
| KNN k=7 | 0.5000 |
| Naive Bayes | 0.4000 |
| Árbol de Decisión | 0.7000 |
| Árbol de Decisión max_depth=5 | 0.6333 |
| Random Forest | 0.6000 |

## Mejor modelo obtenido

El mejor modelo obtenido fue un **Árbol de Decisión**, con un accuracy de:

```text
0.7000
```

La matriz de confusión obtenida fue:

```text
[[13  2]
 [ 7  8]]
```

Este resultado indica que el modelo clasificó correctamente el **70%** de las muestras del conjunto de prueba. Además, se observa un mejor desempeño en la identificación de la clase negativa que en la clase positiva, por lo que existe oportunidad de mejora en la detección de imágenes con presencia de arroz.

## Instalación de dependencias

Para instalar las dependencias necesarias, ejecutar:

```bash
pip install -r requirements.txt
```

## Ejecución del proyecto

Los scripts fueron desarrollados y ejecutados en Google Colab. Para reproducir el flujo completo, se recomienda ejecutar los archivos en el siguiente orden:

```bash
python src/proyecto_arroz.py
python src/conjunto_datos.py
python src/eval_modelos.py
```

## Archivos de documentación

- `DATASET.md`: describe la recolección, estructura, procesamiento y limitaciones del conjunto de datos.
- `MODEL_CARD.md`: documenta el modelo seleccionado, métricas, limitaciones, uso previsto y reproducibilidad.
- `requirements.txt`: contiene las librerías necesarias para ejecutar el proyecto.
- `LICENSE`: indica las condiciones de uso del código del repositorio.

## Autor

**Felipe Ulate Rodríguez**  
**Carné:** C37925  
Universidad de Costa Rica  
IE0435 - Inteligencia Artificial Aplicada a la Ingeniería Eléctrica
