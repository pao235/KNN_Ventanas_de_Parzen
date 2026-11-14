# KNN y Ventanas de Parzen · Clasificación de Cáncer de Mama

**Clasificadores no paramétricos implementados desde cero en Python**
Inteligencia Artificial · ITCH · Semestre enero–junio 2026

![Plataforma](https://img.shields.io/badge/Plataforma-Google%20Colab-orange)
![Lenguaje](https://img.shields.io/badge/Lenguaje-Python-blue)
![Algoritmos](https://img.shields.io/badge/Algoritmos-KNN%20%7C%20Parzen-purple)
![Estado](https://img.shields.io/badge/Estado-Completado-brightgreen)

[![Abrir en Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/pao235/KNN_Ventanas_de_Parzen/blob/main/KNN_y_Ventanas.ipynb)

---

## Descripción

Cuaderno de Jupyter que implementa y compara dos métodos de clasificación no paramétricos:

- **K-Nearest Neighbors (KNN):** clasifica por mayoría entre los *k* vecinos más cercanos.
- **Ventanas de Parzen:** clasifica por mayoría entre todos los vecinos dentro de un radio fijo *h*. Si la ventana queda vacía, se usa 1-NN como respaldo.

Ambos algoritmos se programaron manualmente (distancia euclidiana, selección de vecinos, votación por mayoría y accuracy), usando `scikit-learn` solo para normalización, validación cruzada y métricas.

---

## Dataset

**Breast Cancer Wisconsin (Diagnostic)**, del repositorio UCI. Contiene mediciones de núcleos celulares obtenidas de imágenes de aspiración con aguja fina (FNA) de masas mamarias.

| Característica | Valor |
|----------------|-------|
| Instancias | 569 pacientes |
| Atributos | 30 variables numéricas predictoras |
| Clase 1 (Maligno) | 212 casos (37.3 %) |
| Clase 2 (Benigno) | 357 casos (62.7 %) |

---

## Metodología

1. **Preparación de datos:** carga del CSV, codificación de clases (`M` → 1, `B` → 2), eliminación de columnas irrelevantes y normalización con `StandardScaler`.
2. **División:** 70 % entrenamiento / 30 % prueba, con semilla fija para reproducibilidad.
3. **KNN:**
   - Distancia euclidiana en 30 dimensiones.
   - Búsqueda del mejor *k* (valores impares de 1 a 13) con **validación cruzada K-Fold** (3 particiones).
   - Evaluación en el conjunto de prueba: matriz de confusión, reporte de clasificación y comparación contra el promedio de validación cruzada para analizar la estabilidad.
4. **Ventanas de Parzen:**
   - Búsqueda del radio *h* con validación cruzada (5 particiones) y comparación con la regla de **Silverman** multidimensional.
   - Selección interactiva de *h*: Silverman, validación cruzada o valor manual.
   - Evaluación en prueba con matriz de confusión y reporte de clasificación.
5. **Visualizaciones:**
   - Curva de optimización de *k*.
   - Matrices de confusión de ambos modelos.
   - Superficie de decisión de Parzen en 2D.
   - Distribución de clases con histogramas y KDE.

---

## Estructura del repositorio

```
├── KNN_y_Ventanas.ipynb
├── docs/
│   └── Presentacion_KNN_Parzen.pdf
└── README.md
```

---

## Presentación

📊 [Ver presentación (PDF)](docs/Presentacion_KNN_Parzen.pdf)

---

## Cómo ejecutarlo

1. Haz clic en **Abrir en Colab**.
2. Ejecuta **Entorno de ejecución → Ejecutar todo**.
3. Cuando el cuaderno lo pida, responde las entradas interactivas:
   - Usar el *k* sugerido (`s`) o introducir uno propio (`n`).
   - Elegir *h* por Silverman (`s`), validación cruzada (`c`) o manual (`m`).

El dataset se descarga automáticamente desde una URL, así que no necesitas subir archivos. Las librerías necesarias (`pandas`, `numpy`, `scikit-learn`, `matplotlib`, `seaborn`) ya vienen en Colab.

> **Nota:** como KNN y Parzen están implementados con ciclos en Python puro, la optimización de hiperparámetros puede tardar algunos minutos.

---

## Créditos

La estructura base del cuaderno parte del proyecto original [akshayrb22/playing-with-data](https://github.com/akshayrb22/playing-with-data/blob/master/supervised_learning/KNN/KNN.ipynb), adaptado y extendido con la validación cruzada, la implementación de Ventanas de Parzen, la regla de Silverman y las visualizaciones.

## Autores

**Ana Paola Cardona Valenzuela y Emiliano Pérez Dyck** · Inteligencia Artificial · ITCH · Semestre 8

## Licencia

Uso académico.