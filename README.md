# 📊 Análisis de Correlación — NovaRetail+
### Explorando factores de comportamiento del cliente · Sprint 8 · TripleTen Data Analytics

---

## 🗂 Descripción del proyecto

NovaRetail+ es una plataforma de comercio electrónico en Latinoamérica con millones de usuarios activos. Este proyecto responde a la siguiente pregunta de negocio planteada por el equipo de **Crecimiento y Retención**:

> **¿Qué factores del comportamiento del cliente están más fuertemente asociados con el ingreso anual generado?**

El análisis es de tipo **correlacional y exploratorio**. No se asume causalidad en ningún momento.

---

## 📁 Estructura del repositorio

```
novaretail-correlacion/
│
├── novaretail_reporte_correlacion.ipynb   # Notebook principal con el reporte completo
├── README.md                              # Este archivo
└── /img                                  # Visualizaciones exportadas (heatmap, pairplot, scatterplots)
```

---

## 📦 Dataset

| Campo | Detalle |
|---|---|
| Archivo | `novaretail_comportamiento_clientes_2024.csv` |
| Registros | 15,000 filas |
| Columnas | 12 variables |
| Valores nulos | Ninguno |

**Variables incluidas:**

| Variable | Tipo | Descripción |
|---|---|---|
| `edad` | Numérica | Edad del cliente |
| `nivel_ingreso` | Numérica | Ingreso anual estimado del cliente |
| `visitas_mes` | Numérica | Visitas mensuales a la plataforma |
| `compras_mes` | Numérica | Compras realizadas en el mes |
| `gasto_publicidad_dirigida` | Numérica | Inversión publicitaria asignada al usuario |
| `satisfaccion` | Numérica (1–5) | Calificación de satisfacción |
| `ingreso_anual` | Numérica | **Métrica objetivo** — ingreso generado para la empresa |
| `miembro_premium` | Binaria | Suscripción premium (1 = sí, 0 = no) |
| `abandono` | Binaria | Abandonó la plataforma (1 = sí, 0 = no) |
| `tipo_dispositivo` | Categórica | Móvil / Escritorio / Tablet |
| `region` | Categórica | Norte / Sur / Este / Oeste |

---

## 🔬 Metodología

Se aplicaron cuatro métodos de correlación según el tipo de variable:

| Método | Variables | Supuesto |
|---|---|---|
| **Pearson** | Numérica ↔ Numérica | Relación lineal |
| **Spearman** | Numérica ↔ Numérica | Relación monótona, sin supuesto de normalidad |
| **Punto-biserial** | Numérica ↔ Binaria | — |
| **V de Cramér** | Categórica ↔ Categórica | — |

---

## 📈 Visualizaciones

El reporte incluye:
- **Heatmap** con máscara triangular — vista panorámica de todas las correlaciones
- **Pairplot** con KDE en diagonal — pares de variables clave
- **Scatterplot doble** con línea de regresión — los dos pares más relevantes respecto a `ingreso_anual`

---

## 🔎 Hallazgos principales

### Hallazgo 1 — `compras_mes` ↔ `ingreso_anual` · r = 0.967
La correlación más fuerte del dataset. Positiva, casi perfecta y consistente en Pearson y Spearman. Los clientes con mayor frecuencia de compra mensual tienden a asociarse con mayores ingresos anuales para la plataforma.

> ⚠️ Colinealidad severa: no se recomienda usar ambas variables como predictores simultáneos en modelos futuros.

### Hallazgo 2 — `gasto_publicidad_dirigida` ↔ `visitas_mes` · r ≈ 0.58
Correlación positiva moderada-alta. A mayor inversión publicitaria, más visitas registradas. Sin embargo, la correlación directa con `ingreso_anual` es débil (r ≈ 0.20), lo que sugiere que las visitas generadas no siempre se convierten en compras.

> 💡 Hipótesis: existe una cadena `publicidad → visitas → compras → ingreso` donde el eslabón débil es la conversión.

### Hallazgo 3 — `miembro_premium` y `abandono` · Punto-biserial ≈ 0.00
Sin asociación estadística apreciable con `ingreso_anual` a nivel agregado. Estas variables podrían ser más útiles como criterios de segmentación que como predictores directos de ingreso.

---

## ⚠️ Limitaciones

- **Correlación ≠ causalidad.** Ningún hallazgo implica relación causa-efecto.
- **Variables no medidas.** No se incluye valor promedio por transacción, categoría de producto ni antigüedad del cliente.
- **Análisis agregado.** Patrones dentro de subgrupos (premium, región, dispositivo) podrían quedar invisibles.
- **Relaciones no lineales.** Pearson y Spearman no detectan efectos de umbral o de U-invertida.
- **Corte temporal único.** No es posible evaluar estacionalidad ni estabilidad de las asociaciones.

---

## 🚀 Próximos pasos

- **Análisis segmentado** — correlaciones separadas por segmento (premium vs. no premium, región, dispositivo)
- **Análisis de conversión** — explorar tasa visitas → compras como métrica intermedia
- **Detección de no-linealidades** — aplicar *distance correlation* o *mutual information*
- **Análisis de mediación** — evaluar si `visitas_mes` es mediador en la cadena publicidad → ingreso
- **Experimento controlado** — diseñar A/B test para evaluar el componente causal de la publicidad
- **Análisis temporal** — incorporar datos históricos para evaluar estabilidad de correlaciones

---

## 🛠 Stack tecnológico

![Python](https://img.shields.io/badge/Python-3.9-3776AB?style=flat-square&logo=python&logoColor=white)
![Pandas](https://img.shields.io/badge/Pandas-150458?style=flat-square&logo=pandas&logoColor=white)
![Seaborn](https://img.shields.io/badge/Seaborn-visualización-4C72B0?style=flat-square)
![Matplotlib](https://img.shields.io/badge/Matplotlib-visualización-11557C?style=flat-square)
![SciPy](https://img.shields.io/badge/SciPy-estadística-8CAAE6?style=flat-square&logo=scipy&logoColor=white)
![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-F37626?style=flat-square&logo=jupyter&logoColor=white)

---

## 📌 Contexto académico

> Proyecto 7 · Sprint 8: Explorar las conexiones de datos con correlaciones  
> Programa: Data Analyst · [TripleTen](https://tripleten.com)  
> Análisis realizado con fines educativos sobre datos simulados.

---

*Este análisis identifica asociaciones estadísticas entre variables. No establece relaciones de causalidad.*
