# Proyecto1_IE0435

En este repositorio se encuentran los entregables correspondientes al primer avance del Proyecto 1 del curso IE0435 "Inteligencia Artificial Aplicada a la Ingeniería Eléctrica".

## Proyecto 1: Clasificación de Contaminaciones en una Línea de Producción Simulada

## Descripción

Este proyecto consiste en el desarrollo de un sistema de clasificación basado en aprendizaje automático clásico para detectar contaminaciones en una línea de producción simulada. La simulación utiliza imágenes tomadas sobre una hoja blanca, donde la presencia de granos de arroz representa una contaminación positiva, mientras que la ausencia de arroz o la presencia de otros objetos corresponde a una muestra negativa.

En este primer avance se realiza la organización del conjunto de imágenes, el preprocesamiento básico y la conversión de las imágenes a una matriz binaria de unos y ceros.

## Estructura del Proyecto

- `Positivo/`: Carpeta con imágenes que contienen granos de arroz.
- `Negativo/`: Carpeta con imágenes sin arroz o con otros objetos.
- `proyecto_arroz.py`: Script en Python utilizado para procesar las imágenes.
- `matriz_final.csv`: Dataset generado a partir de las imágenes procesadas.

## Procedimiento Técnico

1. **Carga de imágenes:** Se leen las imágenes desde las carpetas `Positivo` y `Negativo`.
2. **Redimensionamiento:** Todas las imágenes se ajustan a un tamaño uniforme de 128x128 píxeles mediante OpenCV.
3. **Conversión a escala de grises:** Las imágenes se transforman a blanco y negro para simplificar el análisis.
4. **Binarización:** Se aplica el método de Otsu para separar el fondo blanco de los objetos presentes en la imagen.
5. **Conversión a unos y ceros:** Se genera una matriz binaria donde el fondo blanco se representa con `1` y la presencia de objeto con `0`.
6. **Vectorización:** Cada matriz de 128x128 píxeles se convierte en un vector fila de 16384 valores.
7. **Etiquetado:** Se agrega una última columna con la etiqueta de clasificación: `1` para imágenes con arroz y `0` para imágenes sin arroz.
8. **Exportación:** El conjunto de datos final se guarda en formato CSV para su posterior uso en modelos de clasificación.

## Autor

Nombre Apellido - Carné  
Estudiante de Ingeniería Eléctrica  
Universidad de Costa Rica
