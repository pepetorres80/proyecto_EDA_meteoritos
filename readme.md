📄 README.md (versión inicial – Fase 0 y Fase 1 completadas)
# 🌠 Análisis Exploratorio de Datos (EDA): Meteorite Landings – NASA

Este proyecto realiza un Análisis Exploratorio de Datos (EDA) del dataset oficial **"Meteorite Landings"** publicado por la **NASA**.  
El objetivo es estudiar la calidad de los datos, explorar sus características principales, realizar una limpieza adecuada y generar visualizaciones básicas para comprender mejor la naturaleza de los meteoritos registrados.

El trabajo sigue estrictamente las fases solicitadas en el ejercicio del Máster de Data Science e IA.

---

## 📁 Estructura del repositorio



proyecto_EDA_meteoritos/
│
├── data/
│ └── meteorite_landings_nasa.csv
│
├── notebooks/
│ └── 01_eda_meteorites.ipynb
│
├── README.md
└── requirements.txt (opcional)


---

## 🛰️ 1. Descripción del dataset

El dataset utilizado es **Meteorite Landings**, publicado por NASA Open Data.  
Contiene información sobre todos los meteoritos documentados hasta la fecha, incluyendo:

- Nombre del meteorito  
- ID  
- Tipo ("Valid", "Relict")  
- Clase (recclass)  
- Masa en gramos  
- Estado ("Fell" vs "Found")  
- Año  
- Latitud y longitud del hallazgo  
- Ubicación geográfica

El archivo original se encuentra en formato CSV y contiene **45.716 registros y 10 columnas**.

---

## 🧪 2. Carga del dataset

El dataset fue cargado desde la ruta local:



data/meteorite_landings_nasa.csv


Se utilizó la librería **pandas** para el procesado inicial y la inspección.

---

## 🔍 3. Exploración inicial (Fase 1)

### ✔️ 3.1 Dimensiones del dataset  
El dataset contiene:

- **45.716 filas**
- **10 columnas**

Perfecto para un EDA completo y manejable.

---

### ✔️ 3.2 Tipos de datos (df.info)

| Columna       | Tipo     | Observaciones |
|---------------|----------|---------------|
| name          | object   | Nombre del meteorito |
| id            | int64    | Identificador único |
| nametype      | object   | Tipo de nombre ("Valid", "Relict") |
| recclass      | object   | Clase del meteorito |
| mass (g)      | float64  | Masa en gramos, contiene nulos |
| fall          | object   | Si cayó ("Fell") o fue encontrado ("Found") |
| year          | float64  | Año, viene sucio y requiere conversión a datetime |
| reclat        | float64  | Latitud con muchos nulos |
| reclong       | float64  | Longitud con muchos nulos |
| GeoLocation   | object   | Coordenadas como cadena, redundante |

---

### ✔️ 3.3 Valores nulos detectados



mass (g) -> 131 nulos
year -> 291 nulos
reclat -> 7315 nulos
reclong -> 7315 nulos
GeoLocation -> 7315 nulos


**Conclusión:**  
El dataset está mayormente completo excepto por las **coordenadas**, donde aproximadamente un 16% de los registros no incluyen información geográfica.  
Esto es normal para registros históricos antiguos o incompletos.

---

### ✔️ 3.4 Duplicados



0 duplicados


El dataset no contiene filas repetidas, por lo que no requiere limpieza en este punto.

---

## 🧭 4. Próximas fases del proyecto

El análisis continuará con las siguientes etapas:

### 🔹 Fase 2: Exploración detallada  
- Distribución de masa  
- Distribución de años  
- Análisis de clases de meteorito  
- Visualización categórica “Fell vs Found”  
- Identificación de outliers  
- Comprobación de incoherencias

### 🔹 Fase 3: Limpieza  
- Conversión de tipos (fecha, coordenadas)  
- Eliminación o tratamiento de nulos  
- Normalización de categorías  
- Eliminación de columnas redundantes

### 🔹 Fase 4: Visualización  
- Histograma de masa  
- Barras “Fell vs Found”  
- Boxplot de masa  
- Mapa global (opcional pero recomendado)

### 🔹 Fase 5: Conclusiones  
- Resumen de hallazgos  
- Calidad del dataset  
- Patrones detectados  

---

## 👨‍💻 Autor
Torres (José Torres Sánchez)  
Máster en Data Science e IA

---

## 📅 Estado actual
**Fase completada:** Carga y exploración inicial  
**Próxima fase:** Exploración detallada de variables (Fase 2)

## 🔎 4. Exploración Detallada (Fase 2)

En esta fase se analizan en profundidad las variables numéricas, categóricas, temporales y geográficas del dataset, con el objetivo de detectar patrones, distribuciones, valores atípicos e incoherencias.

---

### 🧪 4.1 Análisis de la masa (`mass (g)`)

La distribución de masa presenta una **asimetría extrema**:

- El **75%** de los meteoritos pesa **menos de 202 g**.
- La **mediana** es de solo **32.6 g**.
- Sin embargo, el máximo alcanza **60.000.000 g** (60 toneladas), lo que genera una **cola larga** con outliers muy intensos.

Histograma en escala logarítmica → necesario para visualizar correctamente la distribución.

**Conclusión:**  
La masa es una variable fuertemente sesgada y dominada por unos pocos meteoritos extremadamente grandes. Esta característica debe considerarse en cualquier análisis posterior.

---

### 🪂 4.2 Distribución *Fell vs Found*

Resultados:

- **Found:** 44.609 registros (96%)
- **Fell:** 1.107 registros (4%)

**Conclusión:**  
La inmensa mayoría de meteoritos no fueron observados durante su caída, sino encontrados posteriormente. Esto explica también parte de los registros incompletos o con información limitada.

---

### 🧱 4.3 Análisis de clases (`recclass`)

- Existen **más de 400 clases distintas** de meteoritos.
- Sin embargo, la distribución está **muy concentrada**:
  - `L6`, `H5`, `L5`, `H6` y `H4` representan más del **60% de todos los registros**.

**Conclusión:**  
Aunque el dataset contiene una gran variedad de tipos, la mayoría de meteoritos pertenecen a unas pocas clases comunes, mientras que la mayoría de clases son extremadamente minoritarias.

---

### 🕒 4.4 Análisis de la variable temporal (`year`)

Resumen estadístico:

- **Mínimo:** 860  → valor anómalo  
- **Máximo:** 2101 → imposible  
- **Mediana:** 1998  
- **Q1–Q3:** 1987–2003

El histograma muestra:

- Casi ningún registro antes de 1700  
- Aumento progresivo desde 1800  
- Explosión de registros entre **1990 y 2010**, coincidiendo con avances científicos y mejores sistemas de catalogación

**Conclusión:**  
La variable `year` contiene **incoherencias claramente identificables** (años imposibles) y requiere limpieza. Además, está sesgada por el aumento moderno de reportes.

---

### 🌎 4.5 Análisis de coordenadas geográficas

**Latitud (reclat):**  
Todos los valores están dentro del rango válido **[-90, 90]**.

**Longitud (reclong):**  
Se detectan valores **superiores a 180 grados** (máximo = **354.47**), lo cual es **geográficamente imposible**.

**Conclusión:**  
La columna `reclong` contiene errores de formato y deberá limpiarse en la siguiente fase. Aproximadamente un 16% del dataset no tiene coordenadas, lo cual es habitual en registros antiguos.

---

## 🧭 5. Resumen de hallazgos de la Fase 2

- La masa presenta outliers extremos → requiere escalado/log para análisis.
- `Fell vs Found` está fuertemente desbalanceado (96% Found).
- Existen más de 400 clases de meteorito, pero unas pocas dominan el dataset.
- La variable temporal contiene años incorrectos y distribución sesgada por registros modernos.
- Coordenadas:
  - Latitud correcta
  - Longitud con errores (>180°)

**Conclusión general:**  
La Fase 2 revela un dataset rico en información, pero con múltiples incoherencias que deben ser tratadas en la **Fase 3 (Limpieza)** para garantizar una exploración fiable y visualizaciones consistentes.

---
