# 🏋️‍♂️ Guía de Entrenamiento: Limpieza de Datos con Pandas

Este documento resume la misión de rescate del dataset de **Javi**, quien registró sus entrenamientos de forma caótica. Aquí se detallan los pasos para transformar datos "sucios" en información lista para el análisis.

## 📋 El Plan de Acción
La limpieza de datos (Data Cleaning) es el paso fundamental antes de cualquier análisis. Los conceptos clave practicados son:

| Paso | Concepto | Herramienta de Pandas |
| :--- | :--- | :--- |
| **1** | Cargar un archivo CSV | `pd.read_csv()` |
| **2** | Explorar dimensiones | `.shape` |
| **3** | Ver tipos de datos | `.dtypes` |
| **4** | Contar valores nulos | `.isnull().sum()` |
| **5** | Estadísticas básicas | `.describe()` |

---

## 🛠️ Maniobras de Rescate (Ejercicios Clave)

### 👯 1. Eliminación de Duplicados
A veces, un entrenamiento se registra dos veces por error.
* **Detección**: Se usan filtros para encontrar filas idénticas.
* **Acción**: Se aplica `.drop_duplicates()` y se reinicia el índice con `.reset_index(drop=True)`.

### 🕳️ 2. Gestión de Valores Nulos (NaN)
Encontramos huecos en columnas como `Date` y `Calories`.
* **Rellenar**: Para las calorías, se calcula la **media** de la columna y se usa `.fillna()`.
* **Eliminar**: Si falta la fecha (`Date`), la fila no es útil y se elimina con `.dropna(subset=['Date'])`.

### 📅 3. Normalización de Fechas
El dataset presentaba fechas con comillas innecesarias o formatos numéricos inconsistentes.
* **Limpieza**: Se eliminan caracteres extraños con `.str.replace()`.
* **Conversión**: Se transforma la columna al tipo `datetime` usando `pd.to_datetime()`.

### 🚨 4. Corrección de Datos Imposibles
Detectamos errores humanos que rompen la lógica del análisis:
* **Errores tipográficos**: Un entrenamiento de 450 minutos (cuando el real era 45) se corrige con `.replace(450, 45)`.
* **Inconsistencias fisiológicas**: Si el pulso máximo (`Maxpulse`) es menor al pulso normal (`Pulse`), la fila se descarta por ser un dato erróneo.

---

## 🏆 Análisis Final (Resultados)
Una vez limpio el dataset, se pueden responder preguntas críticas como:
* **Gasto total**: Suma de calorías quemadas en todo el periodo.
* **Rendimiento**: Pulso medio durante los entrenamientos.
* **Hitos**: Identificar la fecha exacta con mayor quema calórica mediante `.idxmax()`.

