# DATASET

## Descripción general

El conjunto de datos utilizado en este proyecto corresponde a imágenes de una línea de producción simulada. La simulación se realizó utilizando una hoja blanca como fondo, sobre la cual se colocaron granos de arroz.

Las imágenes con presencia de granos de arroz se consideran muestras positivas, mientras que las imágenes sin arroz o con otros objetos se consideran muestras negativas.

## Recolección de datos

Cada imagen fue clasificada según la presencia o ausencia de granos de arroz:

- Clase `1`: imagen positiva, contiene granos de arroz.
- Clase `0`: imagen negativa, no contiene granos de arroz. Puede contener otros objetos o estar vacía.

El archivo `matriz_final.csv` corresponde al conjunto de datos generado a partir de las imágenes propias del estudiante. Posteriormente, este archivo fue integrado con archivos CSV generados por otros compañeros para construir un conjunto de datos grupal.

## Organización de los datos

La carpeta `data/` contiene los datos utilizados en el proyecto:

```text
data/
├── personal/
│   └── matriz_final.csv
│
├── group_inputs/
│   ├── dataset1.csv
│   ├── dataset2.csv
│   ├── dataset4.csv
│   └── dataset5.csv
│
└── processed/
    └── dataset_grupo_final.csv
