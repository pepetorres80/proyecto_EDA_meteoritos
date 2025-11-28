# 🌠 Proyecto EDA Meteoritos (NASA)

Análisis Exploratorio de Datos (EDA) sobre el catálogo oficial de meteoritos de la **NASA**.  
Este proyecto sigue el flujo completo solicitado en el mini-proyecto: carga, exploración, limpieza, visualización básica y conclusiones.

---

## 1. Dataset

- **Fuente:** NASA Open Data – Meteorite Landings  
  https://data.nasa.gov/Space-Science/Meteorite-Landings/gh4g-9sfh  
- **Archivo usado:** `data/meteorite_landings_nasa.csv`
- **Registros iniciales:** ~45.716  
- **Columnas:** 10

### 1.1 Variables principales

- `name` – Nombre del meteorito  
- `id` – Identificador único  
- `nametype` – Tipo de nombre (casi siempre `Valid`)  
- `recclass` – Clase / tipo de meteorito  
- `mass (g)` – Masa en gramos  
- `fall` – Tipo de registro (`Fell` / `Found`)  
- `year` – Año de caída o hallazgo  
- `reclat`, `reclong` – Latitud y longitud  
- `GeoLocation` – Coordenada original en formato texto

---

## 2. Objetivo del Ejercicio

Realizar un proceso completo de EDA:

1. **Carga** y revisión inicial del dataset.  
2. **Exploración:** nulos, duplicados, distribuciones, incoherencias y rangos.  
3. **Limpieza:** corrección de tipos, tratamiento de nulos, normalización y eliminación de datos inválidos.  
4. **Visualización básica:**  
   - Histograma  
   - Gráfico de barras  
   - Visualización adicional relevante  
5. **Conclusiones claras** sobre lo encontrado.  
6. Organización del repositorio según lo pedido en el enunciado.

---

## 3. Flujo de Trabajo Realizado

Todo el análisis se encuentra en:

📓 **`notebooks/01_eda_meteorites.ipynb`**

### 3.1 Carga y vista previa

- Se importa el CSV desde la carpeta `data/`.
- Se revisa estructura, tipos de datos y primeras filas con:
  - `df.head()`
  - `df.shape`
  - `df.info()`

Se incluye en el repo una vista previa de las primeras filas.


### 3.2 Exploración inicial

Se analizan:

- **Valores nulos**
- **Duplicados**
- **Distribuciones numéricas**
- **Valores fuera de rango**
- **Categorías principales**

**Nulos detectados inicialmente:**

- `mass (g)`: 131  
- `year`: 291  
- `reclat` / `reclong` / `GeoLocation`: 7.315  
- No hay duplicados.

---

## 4. Limpieza y Normalización

Decisiones principales (todas explicadas en el notebook):

### 4.1 Masa (`mass (g)`)

- Se eliminan meteoritos sin masa o con masa ≤ 0.  
- Se crea una nueva variable:  
  **`mass_log10 = log10(mass)`**

### 4.2 Año (`year`)

- Conversión a numérico.  
- Eliminación de años incoherentes (futuros o muy anteriores al rango lógico).  
- Se conserva únicamente el rango razonable según distribución.

### 4.3 Coordenadas (`reclat`, `reclong`)

- Eliminación de filas fuera de los rangos:  
  - -90 ≤ latitud ≤ 90  
  - -180 ≤ longitud ≤ 180  

### 4.4 Categorías (`fall`, `recclass`)

- Se mantienen las categorías originales.  
- Se analizan las clases más frecuentes.

Tras la limpieza se obtiene un DataFrame consistente para visualización y análisis.

---

## 5. Visualizaciones

En el notebook se incluyen todas las gráficas.  
En el repositorio se almacenan en la carpeta `images/`.

### 5.1 Histograma (escala log10) – Masa

Analiza la distribución extremadamente sesgada y muestra que aplicar log10 mejora la interpretabilidad.

### 5.2 Gráfico de barras – Fell vs Found

La mayoría de registros son **Found**; los meteoritos **Fell** son minoría pero científicamente muy valiosos.

### 5.3 Top 10 clases (`recclass`)

Permite ver qué tipos dominan el catálogo (L6, H5, L5, H6...).

### 5.4 Evolución por década

Se crea la variable `decade` y se observa un incremento fuerte en los registros a partir del siglo XX, debido al aumento de la actividad científica y la capacidad de catalogación.

### 5.5 Boxplot logarítmico de masa

Visualiza los outliers incluso después de aplicar log10.

### 5.6 Mapa de localizaciones

Representación geográfica global usando latitud y longitud válidas.

---

## 6. Conclusiones del EDA

1. **Calidad del dataset:**  
   Buena, pero con nulos, coordenadas inconsistentes y años erróneos.

2. **Distribución de masa:**  
   Extremadamente sesgada; requiere transformación logarítmica.

3. **Registro Fell/Found:**  
   El dataset está dominado por meteoritos encontrados después (Found).

4. **Clases más frecuentes:**  
   Las condritas ordinarias (L6, H5, L5…) concentran la mayoría de registros.

5. **Temporalidad:**  
   El aumento de registros refleja mejoras en técnicas de catalogación, no un cambio real en impactos.

6. **Sesgo geográfico:**  
   Mayor densidad en zonas urbanas/científicas.  
   No se puede concluir "dónde caen más meteoritos" sin corregir este sesgo.

📌 **Conclusión general:**  
El dataset es valioso y suficientemente complejo para un EDA completo.  
Tras la limpieza queda en un estado óptimo para futuros análisis o modelos.

---

## 7. Estructura del Repositorio

```text
├── data/
│   └── meteorite_landings_nasa.csv
├── images/
│   ├── head_preview.png
│   ├── mass_log_hist.png
│   ├── fall_bar.png
│   ├── top_classes.png
│   ├── meteors_per_decade.png
│   ├── mass_log_boxplot.png
│   └── world_map.png
├── notebooks/
│   └── 01_eda_meteorites.ipynb
└── README.md
```





---

## 8. Cómo Ejecutar el Proyecto

```bash
git clone https://github.com/pepetorres80/proyecto_EDA_meteoritos.git
cd proyecto_EDA_meteoritos
```

### instalar dependencias mínimas:

```bash
pip install pandas numpy matplotlib seaborn dataframe_image
```


### Abrir el notebook:

```
notebooks/01_eda_meteorites.ipynb
```


Ejecutar las celdas en orden.

---

## 9. Trabajo Futuro

1. **Crear variables derivadas (p. ej. continentes o rangos de masa).**

2. **Estudiar únicamente meteoritos Fell.**

3. **Añadir mapas avanzados con cartografía real.**

4. **Intentar un modelo de clasificación usando recclass.**

---

## 10. Autor

José Torres Sánchez

