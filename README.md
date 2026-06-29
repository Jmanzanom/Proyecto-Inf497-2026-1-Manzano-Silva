# Proyecto INF497: Análisis Espacial de Exclusión en Campamentos de Viña del Mar 📍

Este repositorio contiene el notebook y los recursos utilizados para analizar el nivel de aislamiento espacial de los campamentos informales en la comuna de Viña del Mar, Región de Valparaíso. El proyecto aplica técnicas de análisis de datos espaciales y modelos de econometría espacial (Spatial Error Model - SEM) para evaluar cómo la antigüedad del asentamiento y su escala demográfica impactan su distancia a servicios urbanos esenciales.

## 👥 Autores

* 
**José Manzano** 


* 
**Manuel Silva** 



*Proyecto desarrollado en el contexto de la asignatura INF497

---

##  Objetivo del Proyecto

El objetivo principal es cuantificar y modelar la exclusión espacial de los campamentos. Para ello, se calcula la distancia mínima de cada asentamiento a puntos de interés críticos (hospitales, clínicas, colegios y paradas de transporte público). Posteriormente, se evalúa si este nivel de aislamiento responde a patrones espaciales sistemáticos mediante el Índice de Moran y modelos de regresión espacial.

##  Tecnologías y Librerías

El análisis está implementado íntegramente en Python utilizando las siguientes herramientas principales:

* **Manipulación y Análisis de Datos:** `pandas`, `numpy`
* **Análisis y Geometría Espacial:** `geopandas`, `shapely`, `osmnx` (para extracción de nodos OpenStreetMap).
* **Econometría y Estadística Espacial (PySAL):** `esda` (Moran, Moran_Local), `splot.esda` (visualización LISA), `libpysal` (matrices de pesos espaciales), `pysal.model.spreg` (regresión OLS y SEM).
* **Visualización:** `matplotlib`, `seaborn`

##  Estructura de Datos (Carpeta `Fuentes de Datos/`)

Para ejecutar este notebook, los siguientes archivos deben estar presentes en el directorio `Fuentes de Datos/`:

1. 
**`doc.kml`**: Archivo original con las geometrías (puntos y polígonos) de los campamentos, extraído para consolidar los polígonos base.


2. 
**`COMUNA_C17.shp`**: Shapefile con los límites comunales del Censo 2017 para uso cartográfico.


3. 
**`Nomina-Campamentos-Catastro-2022.xlsx`**: Catastro del MINVU utilizado para extraer el año de creación (antigüedad) de cada asentamiento.


4. 
**Datos de OpenStreetMap (API):** Descargados en tiempo real mediante `osmnx` filtrando por las etiquetas `amenity`, `public_transport` y `highway`.



##  Metodología Analítica

El trabajo se divide en las siguientes fases metodológicas:

1. 
**Procesamiento Geométrico:** Parseo de archivos KML en crudo para extraer polígonos, transformación al Sistema de Coordenadas Proyectadas UTM Zona 19S (EPSG:32719) para cálculos en metros precisos.


2. 
**Cálculo de Distancias:** Obtención de la distancia euclidiana mínima desde cada campamento al servicio de infraestructura urbana más cercano.


3. **Análisis Exploratorio Espacial (ESDA):**
* Clasificación de exclusión mediante el algoritmo de rupturas naturales de Fisher-Jenks.


* Cálculo de Autocorrelación Espacial Global mediante el Índice de Moran, confirmando la agrupación espacial de los campamentos aislados.


* Identificación de *Hotspots* de aislamiento mediante clústeres LISA (Moran Local).




4. **Modelamiento Espacial:**
* Ajuste de un modelo Ordinary Least Squares (OLS) y revisión de diagnósticos espaciales (Multiplicadores de Lagrange).


* Implementación de un Modelo de Error Espacial (SEM) final para explicar el aislamiento en función de la escala demográfica (logaritmo de familias) y la consolidación territorial (antigüedad), aislando con éxito la dependencia espacial.





##  Instrucciones de Ejecución

1. Clona este repositorio en tu máquina local.
2. Asegúrate de tener instalado Python 3.10+.


3. Instala las dependencias necesarias. Se recomienda utilizar un entorno virtual:
```bash
pip install pandas matplotlib seaborn geopandas osmnx shapely libpysal esda splot spreg beautifulsoup4 lxml openpyxl

```


4. Inicia Jupyter Notebook o abre el archivo en Google Colab/VSCode y ejecuta las celdas de manera secuencial. Asegúrate de que la carpeta `Fuentes de Datos/` esté en el mismo nivel que el notebook.