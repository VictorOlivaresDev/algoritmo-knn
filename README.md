# Predicción de Rotación de Personal con Algoritmo KNN

## 📝 Descripción del Proyecto

Este proyecto de ciencia de datos tiene como objetivo predecir si un empleado abandonará la empresa (`left`) basándose en diversas características como su nivel de satisfacción, la última evaluación, las horas trabajadas y el tiempo en la compañía. Se utiliza el algoritmo de clasificación **K-Nearest Neighbors (KNN)** para construir y evaluar un modelo predictivo.

---

## 📊 Datos Utilizados

El conjunto de datos proviene del archivo `recursos_humanos.csv` y contiene información sobre empleados. Las características utilizadas para el modelo incluyen:

- **Características Numéricas**:
  - `satisfaction_level`: Nivel de satisfacción del empleado.
  - `last_evaluation`: Calificación de la última evaluación.
  - `average_montly_hours`: Promedio de horas trabajadas al mes.
  - `time_spend_company`: Años de antigüedad en la empresa.
  - `Work_accident`: Si el empleado ha tenido un accidente de trabajo (1) o no (0).
  - `promotion_last_5years`: Si el empleado fue promovido en los últimos 5 años (1) o no (0).
- **Características Categóricas**:
  - `sales`: Departamento del empleado.
  - `salary`: Nivel de salario (bajo, medio, alto).

La variable objetivo a predecir es:

- `left`: Si el empleado abandonó la empresa (1) o no (0).

---

## 🛠️ Técnicas y Metodología

El desarrollo del proyecto siguió los siguientes pasos:

### **1. Preprocesamiento de Datos**

- **Selección de características**: Se eliminó la columna `number_project` por considerarse no relevante para el análisis.
- **Codificación de variables categóricas**: Las columnas `sales` y `salary` se transformaron en variables numéricas mediante la técnica de **one-hot encoding** (`get_dummies`), creando columnas binarias para cada categoría.
- **Normalización**: Se normalizaron todas las características predictoras utilizando la escala **Min-Max**, para asegurar que todas las variables tuvieran un rango comparable y no afectaran desproporcionadamente al modelo.

### **2. División del Conjunto de Datos**

El conjunto de datos se dividió en dos subconjuntos:

- **70% para entrenamiento**.
- **30% para pruebas**.

### **3. Modelado con KNN y Búsqueda de Hiperparámetros**

Se utilizó el algoritmo **K-Nearest Neighbors (KNN)**. Para encontrar el número óptimo de vecinos (`k`), se realizó una búsqueda iterativa probando valores de `k` desde 1 hasta 20. Se evaluó el `score` de cada modelo y se seleccionó el valor de `k` que ofreciera el mejor rendimiento en las métricas de evaluación.

---

## 📈 Resultados y Conclusiones

### **Determinación del `k` Óptimo**

Tras iterar y evaluar diferentes valores de `k`, se determinó que **`k=14`** era el valor óptimo. Aunque otros valores como `k=1` y `k=2` mostraron `scores` altos, `k=14` proporcionó los mejores resultados en las métricas de evaluación más detalladas.

### **Evaluación del Modelo (con k=14)**

El modelo final fue evaluado utilizando las siguientes métricas:

- **Score de Precisión**: 0.9038
- **Matriz de Confusión**:

  - **Verdaderos Negativos (se quedaron y se predijo que se quedarían)**: 3163
  - **Falsos Positivos (se quedaron pero se predijo que se irían)**: 253
  - **Falsos Negativos (se fueron pero se predijo que se quedarían)**: 180
  - **Verdaderos Positivos (se fueron y se predijo que se irían)**: 904

  La matriz muestra un buen número de predicciones correctas en comparación con las incorrectas, lo cual es favorable dado el tamaño del conjunto de datos.

- **Precisión por Clase**:

  - **Precisión "Left" (se fue)**: 0.946
  - **Precisión "Stay" (se quedó)**: 0.781

- **Curva ROC y AUC**:
  - El **área bajo la curva (AUC)** fue de **0.95**, un valor muy cercano a 1, lo que indica que el modelo tiene una excelente capacidad para distinguir entre las dos clases (empleados que se van y empleados que se quedan).

### **Conclusión Final**

El análisis exploratorio inicial mostró que el tiempo en la compañía es un factor influyente en la decisión de los empleados de irse, incluso cuando su nivel de satisfacción es alto.

El modelo KNN con **k=14** demostró ser una herramienta muy eficaz para predecir la rotación de personal, logrando una alta precisión y un excelente poder de clasificación, validado por un AUC de 0.95.
