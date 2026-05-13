# MODEL_CARD.md

# Model Card - Proyecto 1 IE0435

## Model name + version

**Nombre del modelo:** Árbol de Decisión para clasificación de contaminaciones  
**Versión:** 1.0  
**Curso:** IE0435 - Inteligencia Artificial Aplicada a la Ingeniería Eléctrica  


## Intended use / out-of-scope

### Uso previsto

Este modelo fue desarrollado con fines académicos para clasificar imágenes de una línea de producción simulada. Su objetivo es detectar la presencia de granos de arroz como contaminaciones positivas en imágenes tomadas sobre una hoja blanca.

El modelo recibe como entrada un vector binario generado a partir de una imagen de 128x128 píxeles y devuelve una clasificación:

- `1`: imagen con presencia de arroz.
- `0`: imagen sin presencia de arroz.

### Uso fuera de alcance

Este modelo no está diseñado para ser utilizado directamente en una línea de producción real. Tampoco debe emplearse como sistema de inspección industrial sin una validación adicional con mayor cantidad de datos, condiciones de iluminación controladas y pruebas en escenarios reales.

## Data summary

El conjunto de datos utilizado se construyó a partir de imágenes tomadas sobre una hoja blanca. Las imágenes positivas contienen granos de arroz, mientras que las negativas no contienen arroz y pueden incluir otros objetos o estar vacías.

Las imágenes fueron procesadas mediante el script `src/proyecto_arroz.py`, aplicando el siguiente procedimiento:

1. Lectura de imágenes desde carpetas positivas y negativas.
2. Conversión a escala de grises.
3. Redimensionamiento a 128x128 píxeles.
4. Binarización mediante el método de Otsu.
5. Conversión a matriz binaria de unos y ceros.
6. Vectorización de la imagen en una fila de 16384 valores.
7. Adición de una etiqueta final.

La codificación utilizada fue:

- `1`: fondo blanco.
- `0`: presencia de objeto.
- Etiqueta `1`: imagen positiva con arroz.
- Etiqueta `0`: imagen negativa sin arroz.

El conjunto final utilizado para evaluación se generó integrando archivos CSV individuales del grupo mediante el script `src/conjunto_datos.py`.

## Labeling process

El etiquetado se realizó manualmente según el contenido visible de cada imagen:

- Las imágenes con granos de arroz fueron etiquetadas como clase `1`.
- Las imágenes sin arroz, vacías o con otros objetos fueron etiquetadas como clase `0`.

La consistencia del etiquetado depende de que cada archivo CSV individual haya seguido la misma convención de clases y la misma codificación binaria de píxeles.

## Models evaluated

Se evaluaron diferentes modelos clásicos de clasificación utilizando el script `src/eval_modelos.py`.

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

## Metrics

El conjunto de datos fue dividido en una proporción de 80% para entrenamiento y 20% para prueba, utilizando `random_state=42` y estratificación por clase.

El mejor modelo obtenido fue:

```text
Árbol de Decisión
Accuracy: 0.7000
```

Matriz de confusión:

```text
[[13  2]
 [ 7  8]]
```

Reporte de clasificación:

```text
              precision    recall  f1-score   support

           0       0.65      0.87      0.74        15
           1       0.80      0.53      0.64        15

    accuracy                           0.70        30
   macro avg       0.73      0.70      0.69        30
weighted avg       0.72      0.70      0.69        30
```

## Ethical/safety notes

El modelo fue desarrollado únicamente con fines académicos. Debido a que el conjunto de datos fue generado en una simulación controlada, pueden existir sesgos relacionados con iluminación, fondo, cámara, sombras, posición de los objetos y variaciones entre las imágenes de cada estudiante.

En un contexto industrial real, un falso negativo podría implicar que una contaminación no sea detectada, mientras que un falso positivo podría generar rechazos innecesarios. Por esta razón, el modelo no debe utilizarse para toma de decisiones críticas sin validación adicional.

## Limitations

Las principales limitaciones del modelo son:

- Tamaño reducido del conjunto de datos.
- Variaciones en iluminación y sombras.
- Diferencias entre cámaras utilizadas.
- Posibles inconsistencias en la captura de imágenes.
- Objetos pequeños que pueden confundirse con arroz.
- Sensibilidad a la posición y orientación de los granos.
- Uso de píxeles binarios como entrada, sin extracción avanzada de características.
- Accuracy moderado de 0.70, por lo que todavía existe margen de mejora.

Además, el modelo presentó mejor desempeño para la clase negativa que para la clase positiva, lo cual indica que puede fallar en algunos casos al detectar imágenes con presencia de arroz.

## Reproducibility

El proyecto fue desarrollado y probado en Google Colab.

Para reproducir el flujo completo, se deben ejecutar los scripts en el siguiente orden:

```bash
python src/proyecto_arroz.py
python src/conjunto_datos.py
python src/eval_modelos.py
```

Las dependencias necesarias se encuentran en el archivo:

```bash
requirements.txt
```

El mejor modelo fue exportado en formato `.joblib` como:

```text
models/mejor_modelo.joblib
```

## Hardware used

Los scripts fueron ejecutados en Google Colab, utilizando el entorno estándar de Python disponible en la plataforma. No se utilizó GPU de forma específica, ya que los modelos evaluados corresponden a algoritmos clásicos de aprendizaje automático.
