[README.md](https://github.com/user-attachments/files/21776084/README.md)
# Taller de Título — Downscaling estadístico espacio–temporal con modelo GTWR

Este repositorio contiene el código y análisis desarrollados para la tesis **"Downscaling estadístico espacio-temporal con modelo GTWR en campos de intensidad del viento en la región de Valparaíso"**, realizada por **Alonso Lagos**.

El análisis principal se encuentra en el archivo `TallerdeTitulo.Rmd` y aborda la estimación de campos de viento a alta resolución (1 km) a partir de datos de menor resolución (3 km) usando técnicas de regresión ponderada geográficamente espacio–temporal (GTWR).

## 📄 Contenido del repositorio

- `TallerdeTitulo.Rmd` — Documento R Markdown con todo el flujo de análisis: carga de datos, exploración, modelado y visualización.
- Scripts auxiliares (si se incluyen) con funciones de apoyo.
- Carpeta de datos (opcional, según disponibilidad).

## 📋 Librerías utilizadas

Este análisis requiere instalar los siguientes paquetes de R:

```r
install.packages(c(
  "ncdf4", "tidyverse", "conflicted", "dplyr", "fields", "maps", "class",
  "lattice", "latticeExtra", "stringr", "FNN", "scales", "ggplot2",
  "reshape2", "RColorBrewer", "gridExtra", "GGally", "psych", "viridis", "grid",
  "ggpubr", "ggcorrplot", "xtable", "bigmemory", "geosphere"
))
```

## ▶️ Ejecución del análisis

1. Clonar este repositorio:
   ```bash
   git clone https://github.com/TU_USUARIO/TU_REPO.git
   cd TU_REPO
   ```

2. Abrir `TallerdeTitulo.Rmd` en **RStudio**.

3. Configurar el directorio de trabajo en R:
   ```r
   setwd("ruta/a/la/carpeta")
   ```

4. Ejecutar los chunks de código en orden o compilar el documento con:
   - **Knit** → HTML / PDF / Word.

## 📊 Metodología
La metodología consiste en tomar campos de viento de modelos WRF y aplicar la relación mediante un modelo de downcaling estadístico que recupero el factor de escala entre las mallas: 3km → 1km → 1/3km.
- **Datos**: [Campos de Viento](https://github.com/Arcanist23/ProyectoDownscalingGTWR_V1/tree/main/data) de viento en mallas espaciales de 3 km y 1 km de resolución, almacenados en formato NetCDF.
- **Modelo**: GTWR (Geographically and Temporally Weighted Regression) para capturar variaciones espaciales y temporales en la relación entre las dos resoluciones. La ejecución del modelo está en la clase de R GTWRbase que contiene los método secuenciales para aplicar el modelo: 1) Constuir matriz de pesos $W$ con $X_{v_3}^{(3)}$; 2) Estimar $\beta$ no-paramétrico; 3) Predecir Campo de viento a resolución 1km.
- **Análisis**:
  - Exploración y visualización de mallas espaciales.
  - Clasificación espacial FPC para distancias distribucionales
  - Análisis descriptivo de los clusters (vecindades representativas)
  - Ajuste de modelos GTWR.
    - Evaluación de campos de vientos.
    - Evaluación de residuos y su estacionariedad local temporal.
    - Selección de ancho de banda $h$
  - Aplicación del esquema a la malla objetivo de $1/3$ km
  - Comparación campos de viento 3km, 1km y 1/3km

## 📜 Licencia

Este repositorio está bajo la licencia MIT — ver el archivo `LICENSE` para más detalles.

## ✍️ Autor

**Alonso Lagos**  
Tesis desarrollada en el marco del Taller de Título — [Universidad de Valparaíso].
