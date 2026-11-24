# Modelo Predictivo de Fatiga y Carga Óptima en Atletas de Wushu Sanda

Proyecto académico desarrollado para la asignatura **Electiva Técnica I**, enfocado en el análisis de datos fisiológicos y de rendimiento deportivo, el entrenamiento de un modelo de clasificación con Machine Learning (`Random Forest`).

## Descripción del Problema y Objetivo
En deportes de combate como el **Wushu Sanda**, equilibrar la intensidad del entrenamiento con la recuperación es clave para prevenir lesiones y sobrecargas. En este proyecto se busca:
1. Analizar las relaciones entre métricas fisiológicas, carga de sesión y descanso.
2. Entrenar un modelo supervisado capaz de clasificar el estado de carga óptima (`Optimal_Load_Class`: **Low**, **Medium**, **High**).
3. Traducir los indicadores principales del modelo a una interfaz de monitoreo visual en **Figma**.

## Dataset Utilizado
* **Fuente:** Kaggle (`datresearch/training-load-and-performance-dataset`), cargado directamente en Google Colab mediante `kagglehub`.
* **Datos:** **4,000 registros** y **22 columnas** (sin valores nulos en las variables principales).
* **Categorías de variables:**
  * **Fisiología y recuperación:** `Resting_HR`, `Training_HR`, `HRV`, `SpO2`, `Sleep_Quality`, `Sleep_Duration`, `Fatigue_Index`.
  * **Carga y sesión:** `Training_Load`, `Session_RPE`, `Session_Duration`, `Repetitions`, `Sets`, `Distance_Covered`.
  * **Rendimiento:** `Movement_Speed`, `Reaction_Time`, `Accuracy`, `Strength_Power`, `Endurance`, `Performance_Score`.
  * **Variable objetivo:** `Optimal_Load_Class` (`Low`, `Medium`, `High`).

## Stack Tecnológico
* **Entorno:** Google Colab (integrado con GitHub).
* **Lenguaje:** Python 3.
* **Librerías principales:** `pandas`, `numpy`, `matplotlib`, `seaborn`, `scikit-learn`, `kagglehub`.

## Metodología y Hallazgos Principales

1. **Análisis Exploratorio:**
   * **Balance de clases:** Las tres categorías de `Optimal_Load_Class` presentan una distribución equilibrada (~1,300–1,360 registros por clase), evitando sesgos por desbalanceo.
   * **Correlación de Pearson (-1 a 1):** Se identificó una correlación negativa moderada-fuerte entre `Sleep_Quality` y `Fatigue_Index` (**-0.63**), confirmando que a mayor calidad de sueño disminuye la fatiga acumulada, y una correlación positiva moderada entre `Training_HR` y `Fatigue_Index` (**0.48**).

2. **Modelado Predictivo (`RandomForestClassifier`):**
   * División estratificada **80 % entrenamiento / 20 % prueba** (800 registros de prueba) con estandarización mediante `StandardScaler`.
   * **Importancia de variables:** En la evaluación inicial, `Sleep_Quality` concentró el mayor peso relativo (~53 %), seguida de `Training_HR` (~28 %) y `Fatigue_Index` (~18 %).
   * **Evaluación:** El modelo base obtuvo una precisión global (*Accuracy*) de **33.50 %** sobre las tres clases balanceadas (cercano al baseline aleatorio de 33.33 %), lo que motivó el análisis comparativo por clase (`groupby`) y la evaluación con el conjunto completo de variables numéricas.

## Enlaces del Proyecto
- **Dataset en Kaggle:** https://www.kaggle.com/datasets/zara2099/training-load-and-performance-dataset
- **Archivos del Proyecto en Drive:** https://drive.google.com/drive/folders/11R4BSgMcCEO9d6A7icVNWhtmvCtSkr-7?usp=sharing
- **Cuaderno en Google Colab (`src.ipynb`):** [src.ipynb](./src.ipynb)
