---
title: "Optimización del Rendimiento en Procesos de Biofabricación"
date: 2026-10-19
summary: "Predicción y optimización del Yield en manufactura biofarmacéutica empleando modelos predictivos en alta dimensión (Lasso, Ridge, PCR, PLSR)."
tags: ["R", "Machine Learning", "glmnet", "pls"]
---

## Descripción General
El presente proyecto se centra en la predicción y optimización del rendimiento (*Yield*) en un proceso de manufactura biofarmacéutica empleando técnicas avanzadas de Machine Learning. El reto principal abordado es el escenario matemático de alta dimensionalidad (p grande frente a n) típico en la bioingeniería, donde los datos presentan una multicolinealidad severa. Esto provoca que los modelos de Regresión Lineal Múltiple clásica (MCO) sufran de varianza inflada y sobreajuste. Para resolverlo, este estudio implementa arquitecturas de regularización (restricción del espacio de hipótesis) y reducción de dimensionalidad, contrastando su efectividad para aislar los factores críticos que maximizan la producción y aportando valor analítico para la toma de decisiones y el escalado industrial.

## Conjunto de Datos
El estudio se realiza sobre un archivo de datos denominado `yield_phrama.csv`. 
- **Dimensiones:** n = 176 observaciones y p = 57 variables predictoras continuas.
- **Variable Objetivo:** `Yield` (Rendimiento del proceso biofarmacéutico).
- **Características:** Las variables independientes engloban métricas altamente dimensionales, combinando características de los materiales biológicos (ej. `BiologicalMaterial02`, `04`, etc.) y variables de control de procesamiento (ej. `ManufacturingProcess29`).

## Desarrollo y Metodología

### Limpieza y Preparación de Datos
El proceso de preprocesamiento se diseñó para garantizar la viabilidad y estabilidad de los modelos matemáticos en alta dimensión:
1. **Diagnóstico y Tratamiento de Valores Ausentes:** La exploración inicial detectó 106 valores nulos (`NA`) dispersos en el conjunto de datos. Al ser un volumen crítico que comprometería el análisis dado el tamaño muestral reducido (n=176), se aplicó una imputación de valores faltantes iterando sobre cada columna e inyectando la **media aritmética** respectiva (`mean(..., na.rm = TRUE)`). Esto permitió conservar todas las observaciones sin sesgar la tendencia central.
2. **Verificación Estructural:** Se confirmó a través de `str()` que ninguna de las 57 variables era categórica, asegurando compatibilidad nativa con las operaciones matriciales posteriores.
3. **Partición de Datos:** Utilizando una semilla de reproducibilidad (`set.seed(123)`), el conjunto se dividió aleatoriamente en:
   * **Training Set (70%):** 123 observaciones para entrenar los modelos.
   * **Testing Set (30%):** 53 observaciones para validar la capacidad de generalización.

### Análisis Exploratorio y Visualización
La comprensión del espacio de los datos se apoyó en técnicas de reducción y visualizaciones enfocadas en el *Yield*:
1. **Análisis de Cargas (Loadings):** Se examinaron los pesos absolutos de las dos primeras componentes para determinar qué características influyen más, aislando el top 10 de variables.
2. **Proyección en el Espacio Latente:** Se generaron gráficos de dispersión (2D) usando `ggplot2` mapeando las Componentes Principales 1 y 2 (para PCR) y las Variables Latentes 1 y 2 (para PLSR). 
3. **Gradiente de Rendimiento:** A cada punto se le aplicó un gradiente de color basado en la variable `Yield` (de azul a rojo).

### Modelado y Pruebas Estadísticas
Se aplicaron cuatro enfoques avanzados, divididos en dos grandes estrategias:

**A. Técnicas de Regularización (glmnet)**
- **Lasso (Penalización L_1, λ = 1):** Ajustado mediante validación cruzada. El modelo final logró producir esparsidad, aislando el ruido al reducir la dimensión de 57 a solo **31 predictores activos**.
- **Ridge (Penalización L_2, λ = 0):** Logró estabilizar los coeficientes frente a la multicolinealidad, pero mantuvo los **57 predictores** originales.

**B. Técnicas de Reducción de Dimensionalidad (pls)**
- **PLSR (Regresión de Mínimos Cuadrados Parciales):** Método supervisado. Requirió únicamente **4 componentes latentes** óptimos para modelar el proceso.
- **PCR (Regresión de Componentes Principales):** Método no supervisado. Requirió **19 componentes principales** óptimos para capturar la señal objetivo de `Yield`.

## Conclusiones y Hallazgos
- **Mejor Capacidad Predictiva:** El modelo **PCR** logró la mayor capacidad predictiva global en el conjunto de prueba (RMSE = 1.430).
- **Mejor Valor Operativo y Simplicidad:** **Lasso** destacó como la alternativa más valiosa para la toma de decisiones, logrando descartar 26 variables irrelevantes.
- **Factores Determinantes Aislados:** El análisis de las cargas bajo PLSR demostró que la calidad de los materiales biológicos y el parámetro de control `ManufacturingProcess29` son los verdaderos factores críticos.

## Reproducibilidad y Gestión de Dependencias
Este proyecto fue desarrollado en **R (4.3.x)**. Para replicar el entorno de desarrollo original, utiliza el siguiente código en R:

```R
# Instalar el gestor de versiones si no está disponible
if (!requireNamespace("remotes", quietly = TRUE)) {
  install.packages("remotes")
}

# Instalación de dependencias con versiones fijadas
remotes::install_version(
  "glmnet", 
  version = "4.1-8", 
  repos = "http://cran.us.r-project.org"
)
remotes::install_version(
  "pls", 
  version = "2.8-3", 
  repos = "http://cran.us.r-project.org"
)
remotes::install_version(
  "ggplot2", 
  version = "3.4.4", 
  repos = "http://cran.us.r-project.org"
)