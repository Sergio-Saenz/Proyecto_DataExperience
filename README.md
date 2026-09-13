# Proyecto Dataxperience

## Análisis de rentabilidad y riesgo de desabastecimiento en el sector farmacéutico colombiano durante 2025

### Integrantes

- Sara Sofía Cruz Fandiño
- Martin Felipe Diaz Collas
- Sergio David Vargas Sáenz
- Julián Fernando Gómez Escobar

---

## 1. Contexto del proyecto

El proyecto analiza un registro de operaciones farmacéuticas correspondiente al año 2025 en Colombia. El interés del análisis surge de la necesidad de comprender cómo diferentes características de las operaciones farmacéuticas pueden relacionarse con la rentabilidad y el riesgo de desabastecimiento, con el fin de identificar patrones útiles para decisiones de ventas, inventario y abastecimiento.

## 2. Objetivo general

Analizar la relación entre el tipo de institución, el fabricante y la ubicación geográfica con la rentabilidad y el riesgo de desabastecimiento de productos farmacéuticos durante 2025, con el propósito de identificar patrones que puedan apoyar la toma de decisiones relacionadas con ventas, inventario y abastecimiento.

## 3. Pregunta principal

¿Cómo se relacionan el tipo de institución, el fabricante y la ubicación geográfica con la rentabilidad y el riesgo de desabastecimiento de productos farmacéuticos durante 2025, y qué patrones pueden apoyar la toma de decisiones sobre ventas, inventario y abastecimiento?

### Preguntas de apoyo

1. ¿Qué tipos de institución presentan mayores niveles de ventas, rentabilidad y margen bruto?
2. ¿Qué fabricantes concentran mayores niveles de ventas y cuáles presentan mejores niveles de rentabilidad?
3. ¿Qué ciudades o regiones presentan mayores niveles de ventas y rentabilidad, y cómo se relacionan con el riesgo de desabastecimiento?
4. ¿Qué relación existe entre los días de inventario, el tiempo de entrega y el riesgo de desabastecimiento?
5. ¿Qué productos o segmentos presentan una combinación de alta rentabilidad y alto riesgo de desabastecimiento?

## 4. Datos utilizados

**Archivo:** `dataset_farmaceutico.csv`
**Registros:** 5.075 operaciones (antes de la limpieza)
**Variables:** 33
**Separador:** `;` | **Codificación:** UTF-8-SIG

### Variables del dataset

| Categoría | Variables |
|---|---|
| Identificación y tiempo | `ID_Registro`, `Fecha`, `Año`, `Mes_Num`, `Mes`, `Trimestre` |
| Ubicación | `Región`, `Ciudad` |
| Institución | `Tipo_Institución`, `Institución`, `Canal` |
| Producto | `Línea_Terapéutica`, `Producto`, `Fabricante`, `Unidad_Medida`, `Requiere_Receta` |
| Operación comercial | `Unidades`, `Precio_Unitario_USD`, `Costo_Unitario_USD`, `Descuento_Pct` |
| Inventario y abastecimiento | `Lead_Time_Días`, `Inventario_Días`, `Devolución_Pct`, `Pacientes_Impactados`, `Urgencia_Abasto` |
| Resultados financieros | `Ventas_Brutas_USD`, `Monto_Descuento_USD`, `Ventas_Netas_USD`, `Costo_Total_USD`, `Utilidad_Bruta_USD`, `Margen_Bruto_Pct` |
| Riesgo | `Devoluciones_Unidades`, `Riesgo_Stockout` |

## 5. Estructura del notebook

El análisis está desarrollado en `Proyecto_dataxperience.ipynb`, organizado en las siguientes secciones:

1. **Contexto, objetivo y preguntas de investigación**
2. **Datos utilizados** — fuente y descripción de variables
3. **Carga y revisión inicial de los datos** — dimensiones, tipos de datos, valores faltantes, duplicados, revisión de variables categóricas y numéricas sobre los datos crudos
4. **Limpieza de los datos** — eliminación de duplicados, corrección de formatos de fecha, normalización de la ubicación geográfica, de variables categóricas (región, tipo de institución, canal, línea terapéutica, unidad de medida, receta) y de variables numéricas, seguida de una auditoría final
5. **Análisis Exploratorio de Datos (EDA)** — comportamiento de ventas, rentabilidad por institución/fabricante/ubicación, relación entre inventario, lead time y riesgo de desabastecimiento, productos con alta rentabilidad y alto riesgo
6. **Patrones y posibles respuestas** a las preguntas de investigación
7. **Comparación crudo vs. limpio** — impacto de la limpieza en las conclusiones
8. **Conclusiones preliminares y próximos pasos**
9. **Estadística descriptiva** — tendencia central, dispersión, forma de la distribución, valores atípicos, comparación por segmentos
10. **Modelado predictivo**:
    - **Modelo 1 (Regresión):** OLS, Ridge y Lasso para predecir `Margen_Bruto_Pct`
    - **Modelo 2 (Clasificación):** Random Forest para predecir `Riesgo_Alto` (variable binaria derivada de `Riesgo_Stockout` según su mediana), incluyendo matriz de confusión e importancia de variables
    - Interpretación comparativa de ambos modelos
11. **Conclusiones y referencias**

## 6. Principales resultados

- **Calidad de datos:** se detectaron 50 duplicados exactos, valores faltantes en campos clave (institución, fabricante, ciudad, región) e inconsistencias de formato en variables categóricas (mayúsculas/minúsculas, tildes).
- **Modelo de regresión (rentabilidad):** OLS y Ridge obtuvieron un desempeño prácticamente idéntico (R² ≈ 0,70, MAE ≈ 0,045), superando a Lasso (R² ≈ 0,36). Se seleccionó **OLS** como modelo final.
- **Modelo de clasificación (riesgo de desabastecimiento):** el **Random Forest** alcanzó Accuracy 97,10%, Precision 96,08%, Recall 98,20% y F1-score 97,13%. Las variables más importantes fueron `Lead_Time_Días` e `Inventario_Días`.

## 7. Requisitos

- Python 3
- Librerías: `pandas`, `numpy`, `matplotlib`, `scikit-learn` (`sklearn.linear_model`, `sklearn.ensemble`, `sklearn.model_selection`, `sklearn.preprocessing`, `sklearn.compose`, `sklearn.pipeline`, `sklearn.metrics`)

Instalación rápida:

```bash
pip install pandas numpy matplotlib scikit-learn
```

## 8. Cómo ejecutar

1. Ubicar `dataset_farmaceutico.csv` en la misma carpeta que el notebook.
2. Abrir `Proyecto_dataxperience.ipynb` en Jupyter Notebook, JupyterLab o Google Colab.
3. Ejecutar las celdas en orden: primero la carga y limpieza de datos, luego el EDA, la estadística descriptiva y finalmente los modelos predictivos.

## 9. Estructura de archivos

```
├── Proyecto_dataxperience.ipynb   # Notebook con el análisis completo
├── dataset_farmaceutico.csv       # Dataset original (crudo)
└── README.md                      # Este archivo
```

## 10. Referencias

- Dataset obtenido del repositorio de GitHub: https://github.com/dvillamil857/dataset-farmaceutico-colombia
