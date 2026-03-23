# Análisis de Deserción Laboral — IBM HR Analytics

Proyecto de análisis de datos desarrollado como segundo evento evaluativo del curso.
El objetivo es explorar, analizar y preprocesar el dataset de IBM HR Analytics para
comprender qué factores llevan a un empleado a renunciar, sentando las bases para
un futuro modelo predictivo de deserción laboral.

---

## Estructura del repositorio

```
├── Data/
│   └── WA_Fn-UseC_-HR-Employee-Attrition.csv
├── Analisis_Exploratorio/
    └──ExploracionBasesdeDatos.ipynb
    └──EDA.ipynb
    └──03_Preprocesamiento_Reduccion.ipynb
└── README.md
```

---

## Dataset seleccionado

**IBM HR Analytics Employee Attrition & Performance**
- Fuente: [Kaggle](https://www.kaggle.com/datasets/pavansubhasht/ibm-hr-analytics-attrition-dataset)
- Tipo: Tabular, secundario
- Registros: 1,470 empleados | Atributos: 35 variables (26 numéricas, 9 categóricas)
- Tamaño: 227.98 kB
- Variable objetivo: `Attrition` (Yes/No) — 16.1% de casos positivos

---

## Fases del proyecto

### Fase 1 — Exploración de Bases de Datos
**Notebook:** `ExploracionBasesdeDatos.ipynb`

Se exploraron tres datasets de dos tipos diferentes antes de seleccionar el dataset final:

| Dataset | Tipo | Registros | Tamaño |
|---|---|---|---|
| IBM HR Analytics | Tabular | 1,470 | 227.98 kB |
| Stack Overflow Developer Survey | Tabular | +80,000 | 94.84 MB |
| Reptiles and Amphibians Images | Imágenes | ~6,045 | 141.05 MB |

El dataset de IBM HR Analytics fue seleccionado con base en cuatro criterios: completitud
(cero valores nulos), relevancia del problema, nivel de documentación disponible y
manejabilidad computacional.

---

### Fase 2 — Análisis Exploratorio de Datos (EDA)
**Notebook:** `EDA.ipynb`

EDA completo sobre el dataset de IBM HR Analytics, estructurado en las siguientes secciones:

- **2.1 Valores faltantes:** Verificación de nulos y estrategia de tratamiento propuesta
  por rangos de porcentaje (eliminación, imputación, indicador binario).
- **2.2 Detección de outliers:** Boxplots, cálculo IQR y z-score para 7 variables clave.
  Decisión documentada de conservar outliers por ser perfiles laborales legítimos.
- **2.3 Análisis de distribuciones:** Histogramas con KDE para 9 variables numéricas.
  Clasificación por nivel de sesgo e identificación de candidatas a transformación logarítmica.
- **2.4 Análisis univariado:** Estadísticos descriptivos (media, mediana, CV%, skew) y
  gráficos de barras para las 7 variables categóricas.
- **2.5 Análisis multivariado:** Tablas cruzadas categóricas y ordinales vs Attrition,
  mapa de calor de correlaciones, correlación directa con la variable objetivo,
  pairplot y diagramas de dispersión.
- **2.6 Hipótesis iniciales:** 5 hipótesis verificables planteadas a partir del EDA.
- **2.7 Insights principales:** 7 insights que cubren patrones relevantes, problemas
  de calidad detectados y líneas de análisis para fases posteriores.

**Principales hallazgos:**
- `OverTime=Yes` triplica la tasa base de deserción (~30% vs ~10%)
- Los empleados en sus primeros 2 años concentran el mayor riesgo de abandono
- `MonthlyIncome` y `TotalWorkingYears` son los predictores numéricos con mayor
  correlación negativa con Attrition
- El departamento de Ventas presenta la mayor tasa de rotación relativa
- El dataset está desbalanceado (16.1% positivos), lo que requerirá técnicas
  especiales en el modelado

---

### Fase 3 — Preprocesamiento y Reducción de Dimensionalidad
**Notebook:** `03_Preprocesamiento_Reduccion.ipynb`

Pipeline completo de preparación de datos para modelado:

- **3.1 Limpieza:** Eliminación de 4 columnas con valor constante (`EmployeeCount`,
  `EmployeeNumber`, `Over18`, `StandardHours`).
- **3.2 Codificación:** Label Encoding para variables binarias (`Gender`, `OverTime`,
  `Attrition`) y One-Hot Encoding para variables nominales de más de 2 categorías
  (`BusinessTravel`, `Department`, `EducationField`, `JobRole`, `MaritalStatus`).
- **3.3 Escalado:** StandardScaler aplicado a todas las features (media=0, std=1).
- **3.4 PCA:** Scree plot de varianza explicada, visualización 2D coloreada por
  Attrition y loading plot con las variables de mayor contribución a cada componente.
  El 90% de la varianza se preserva con una fracción de las columnas originales.

---

## Requisitos

```bash
pip install numpy pandas matplotlib seaborn scikit-learn scipy
```

Los notebooks deben ejecutarse en orden:
1. `ExploracionBasesdeDatos.ipynb`
2. `EDA.ipynb`
3. `03_Preprocesamiento_Reduccion.ipynb`

Cada notebook carga el dataset directamente desde `../Data/` y es autocontenido.

---

## Integrantes del equipo

| Nombre | Contribuciones principales |
|---|---|
| [Carlos Alberto Moreno David] | [Ej: Fase 1, Fase 2 Secciones 2.1–2.2] |
| [Juan Esteban García Ocampo] | [Ej: Fase 2 Secciones 2.3–2.5] |
| [Emiliano Vélez Suárez] | [Ej: Fase 2 Sección 2.5, Hipótesis, insights, README] |
| [Sebastián Ciro Medellín] | [Ej: Fase 3] |