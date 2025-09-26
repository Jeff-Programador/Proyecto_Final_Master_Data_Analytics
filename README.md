# 🏡 Proyecto Final – Análisis de Mercado Inmobiliario

https://drive.google.com/file/d/1N1VEpjbOR-RRLberhkizYP0Nf0g2FgmA/view?usp=sharing
link de los archivos, comprimidos

Este proyecto corresponde al **proyecto final de análisis de datos**, cuyo objetivo ha sido realizar un **EDA (Exploratory Data Analysis)** y un **Dashboard interactivo** en Power BI sobre un dataset inmobiliario.

---

## 📂 Estructura del repositorio

house-eda-dashboard/
├─ data/

│ ├─ raw/
│ │ ├─ 1_houses_data.csv # Dataset de propiedades en bruto
│ │ ├─ 2_finance_data.csv # Dataset financiero en bruto
│ │ └─ README.md # Fuentes o URLs de datos

│ └─ processed/
│ ├─ final_house_dataset.xlsx # Dataset combinado
│ └─ final_house_dataset_clean.csv # Dataset limpio tras IQR

├─ notebooks/
│ └─ EDA.ipynb # Análisis exploratorio de datos (Python)

├─ dashboard/
│ └─ Dashboard.pbix # Dashboard en Power BI

├─ reports/
│ └─ EDA.pdf # Informe final del análisis

├─ README.md # Este archivo
└─ requirements.txt # Dependencias de Python


## 🛠️ Proceso seguido

### 1. Obtención de datos
- Se descargaron **dos datasets**:  
  - `1_houses_data.csv` (información de propiedades)  
  - `2_finance_data.csv` (información financiera de los clientes).  
- Posteriormente se **combinaron en un único dataset**: `final_house_dataset.xlsx`.

### 2. Limpieza y transformación
- Se corrigieron formatos de columnas (fechas, categóricas, numéricas).  
- Se eliminaron **outliers extremos con el método IQR**, pasando de **200,000 registros a 87,634**.  
- Código utilizado:

```python
# Identificar columnas numéricas
numerical_columns = dataset.select_dtypes(include=['int64', 'float64']).columns

# Calcular Q1, Q3 e IQR
Q1 = dataset[numerical_columns].quantile(0.25)
Q3 = dataset[numerical_columns].quantile(0.75)
IQR = Q3 - Q1

# Definir límites
lower_bound = Q1 - 1.5 * IQR
upper_bound = Q3 + 1.5 * IQR

# Filtrar dataset limpio
dataset_clean = dataset[~((dataset[numerical_columns] < lower_bound) | 
                          (dataset[numerical_columns] > upper_bound)).any(axis=1)]

# Guardar
dataset_clean.to_csv("final_house_dataset_clean.csv", index=False)


3. Análisis exploratorio de datos (EDA)

Con el notebook EDA.ipynb se realizaron:
Análisis descriptivo de variables.
Visualización de distribuciones (precios, tamaños, salarios, préstamos).
Correlaciones entre variables (heatmap).
Identificación de relaciones clave, como salario vs precio o préstamo vs down payment.
El informe en PDF (EDA.pdf) incluye todas las gráficas y comentarios.

4. Dashboard en Power BI

Se creó un dashboard interactivo con 5 páginas:
KPIs principales → Precio promedio, máx, mín, tamaño promedio, salario promedio, préstamos y down payments.
Distribución del mercado → Histogramas de precios y tamaños, precio por número de habitaciones y baños.
Análisis financiero → Relación salario–precio, préstamos promedio por rango, scatter loan vs down payment, KPI ratio EMI/Ingreso.
Calidad de vida y satisfacción → Precio promedio según rating del vecindario, conectividad y satisfacción del cliente.
Conclusiones finales → Resumen con insights clave del mercado inmobiliario.
Archivo: dashboard/Dashboard.pbix

📊 Resultados principales

El 70% de las propiedades se encuentra entre 300k y 800k → mercado de rango medio.
El precio está altamente correlacionado con el monto del préstamo (0.94), el pago inicial (0.84) y el tamaño de la propiedad (0.76).
Las variables de calidad de vida (satisfacción, rating, conectividad) no tienen impacto directo en el precio, pero sí en la decisión de compra.
El segmento premium/lujo es minoritario, pero relevante, pues genera dispersión y outliers.

📌 Conclusiones finales

El mercado inmobiliario analizado se caracteriza por un predominio de propiedades estándar de rango medio en precio y tamaño.
Los factores financieros y físicos son los principales determinantes del precio, mientras que las variables cualitativas afectan más a la satisfacción del cliente que al valor de la propiedad.
Este análisis proporciona una base sólida para:
Construir modelos predictivos de precio.
Segmentar clientes según capacidad adquisitiva.
Tomar decisiones estratégicas en inversión inmobiliaria.

Requisitos

Instalar dependencias de Python:
pip install -r requirements.txt
Principales librerías utilizadas:
pandas
numpy
matplotlib
scikit-learn


