---
title: "Retail Operations & Discount Impact Dashboard"
date: 2026-10-20
summary: "Análisis integral de operaciones retail en Tableau para evaluar el impacto de los descuentos en la rentabilidad y segmentar el comportamiento de compra."
tags: ["Tableau", "Business Intelligence", "Data Visualization", "Retail Analytics"]
---

## Descripción General
Este proyecto consiste en el diseño y desarrollo de un **Dashboard Ejecutivo en Tableau Public** orientado al análisis de ventas y operaciones de una cadena de *retail* (SuperStore). El objetivo principal es proporcionar una herramienta interactiva que permita a los tomadores de decisiones evaluar la salud financiera del negocio, entender la evolución temporal de los pedidos y diagnosticar cómo las políticas de descuentos afectan directamente a la rentabilidad (*Profit*).

## Conjunto de Datos
El análisis se fundamenta en un dataset transaccional con **casi 10.000 registros históricos** de pedidos realizados entre 2014 y 2017. 
- **Volumen Financiero Analizado:** Ventas totales de **$2.297.201** y un beneficio neto de **$286.397**.
- **Variables Clave:** Fecha de pedido (`Order Date`), Modo de envío (`Ship Mode`), Segmento de cliente (`Segment`), Ventas (`Sales`), Cantidad (`Quantity`), Descuento (`Discount`) y Beneficio (`Profit`).

## Objetivos del Análisis Visual

1. **Impacto de Descuentos en Rentabilidad:** Mediante un diagrama de dispersión (Scatter Plot), se modela la relación entre el volumen de pedidos y el descuento promedio aplicado, permitiendo identificar umbrales de descuento críticos donde el margen de beneficio se degrada o genera pérdidas.
2. **Tendencia Temporal de Operaciones:** Un análisis de series temporales revela el crecimiento interanual del volumen de pedidos, mostrando una evolución alcista que culmina con el pico máximo de actividad en el año 2017.
3. **Segmentación de Clientes y Logística:** 
   - Se evidencia que el segmento dominante es **Consumer** (Consumidor final), superando ampliamente a los segmentos corporativos (*Corporate* y *Home Office*).
   - A nivel logístico, el modo de envío predominante es la clase estándar (*Standard Class*), lo que sugiere una oportunidad para optimizar los costes de envíos *premium* o incentivar ventas cruzadas para mejorar los envíos urgentes.

## Tecnologías Utilizadas
- **Tableau Public:** Construcción del dashboard interactivo, creación de campos calculados, integración de filtros y diseño de la interfaz de usuario (UI).
- **Procesamiento de Datos:** Limpieza y estructuración del archivo fuente estructurado en CSV (`B-Sample-Superstore.csv`), asegurando la integridad de las jerarquías de productos, regiones y fechas.
- **Data Storytelling:** Aplicación de buenas prácticas de visualización ejecutiva, aislando KPIs de alto nivel (Sales y Profit) para una lectura rápida, y acompañando con gráficos de soporte detallados.

---
![Dashboard SuperStore - Retail Operations](/dashboard-superstore.png)
> 📊 **Ver Dashboard Interactivo:** [Acceder al proyecto en Tableau Public](https://public.tableau.com/app/profile/santiago.mart.nez.granda/viz/RetailOperationsDiscountImpactDashboard/Dashboard1)