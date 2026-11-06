---
title: "Segmentación de Clientes & Perfilado de Riesgo Financiero"
date: 2026-10-21
summary: "Aprendizaje no supervisado (K-Means, PCA y DBSCAN) sobre una cartera de 8.950 tarjetas de crédito para identificar patrones de consumo y perfiles de riesgo."
tags: ["Python", "Machine Learning", "Clustering", "PCA", "Scikit-Learn"]
---

## Descripción General
Este proyecto aplica **aprendizaje no supervisado** para segmentar a **8 950 titulares de tarjeta de crédito** a partir de **17 variables de comportamiento transaccional** (saldo, compras, anticipos de efectivo, pagos, límite de crédito, antigüedad, etc.).

**Problema de negocio:** Una entidad financiera que trata a todos sus clientes por igual desperdicia efectividad en sus campañas de marketing y detecta tarde los comportamientos de riesgo. El objetivo es descubrir patrones de uso no evidentes y agruparlos en **segmentos homogéneos, interpretables y accionables**.

**Resultado clave:**
- **Clientes analizados:** 8.950
- **Componentes principales (PCA):** 6 (reteniendo el 80.4% de la varianza)
- **Modelo final:** K-Means (K = 5)
- **Modelo descartado:** DBSCAN (generó 1 macro-clúster con el 99.4% de los datos por densidad continua)

---

## Metodología y Flujo de Trabajo

El flujo de trabajo sigue un *pipeline* deliberado y reproducible:

1. **Calidad de Datos & EDA:** Detección de asimetría positiva severa y multicolinealidad entre variables monetarias.
2. **Preprocesamiento:** Imputación por mediana, transformación logarítmica (`np.log1p`) para mitigar el impacto de *outliers* y escalado estandarizado (`StandardScaler`).
3. **Reducción de Dimensión:** Selección de 6 componentes principales mediante **PCA** para eliminar la redundancia dimensional.
4. **Modelado y Selección:** Evaluación de K mediante el método del codo y el coeficiente de silueta, seleccionando K=5 por interpretabilidad comercial.

---

## Segmentos Finales y Perfilado

| Clúster | % Cartera | Perfil comercial | Rasgos clave (mediana) | Acción prioritaria |
| :---: | ---: | :--- | :--- | :--- |
| **0** | 30.11% | **Inactivos / Revolvers pasivos** | Compras = 0; saldo 1.439; anticipos 939 | Campañas de reactivación y cashback |
| **1** | 22.41% | **VIP / High Spenders** | Compras 1.963; frecuencia 1.00; límite 6.000 | Fidelización premium / tarjeta Black |
| **2** | 9.97% | **Efectivo / Alto riesgo** | Saldo 3.815; anticipos 3.215; pagos mín. 1.298 | Gestión de riesgo y refinanciación |
| **3** | 14.63% | **Bajo uso / Low Engagement** | Saldo 22; compras 177; frecuencia 0.20 | Onboarding y vinculación digital |
| **4** | 22.88% | **Compradores a plazos** | Compras en cuotas 419 vs. 0 pago único | Promociones 0% interés y revisión de límite |

---

## Insights de Negocio
- 🔴 **Riesgo:** El Clúster 2 (≈10%) combina saldos elevados, uso intensivo de efectivo y pagos mínimos altos → prioridad para seguimiento y mitigación de morosidad.
- 🟢 **Valor:** El Clúster 1 (≈22%) concentra el mayor gasto con frecuencia de compra plena → candidato natural a programas de fidelización premium.
- 🟡 **Oportunidad:** El Clúster 0 (≈30%) representa la mayor palanca de reactivación al no realizar compras pero mantener uso de tarjeta.

---
> 💻 **Repositorio del Código:** [Ver proyecto y Notebook en GitHub](https://github.com/santimartiinez)