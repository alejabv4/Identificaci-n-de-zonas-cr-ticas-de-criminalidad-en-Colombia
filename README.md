# Identificación de Zonas Críticas de Criminalidad en Colombia

## Descripción del Proyecto

Proyecto de Big Data para identificar y clasificar zonas críticas de criminalidad en Colombia mediante el análisis de **2,382,453 registros históricos del período 2020-2026**, implementando un sistema de priorización automático por severidad con 5 niveles de criticidad.

## Características Principales

* **Dataset Procesado:** 2.38M registros de criminalidad (2020-2026)
* **Cobertura:** 1,111 municipios analizados
* **Arquitectura:** Medallion (Bronze → Silver → Gold)
* **Clasificación Automática:** 5 niveles de criticidad basados en percentiles
* **Integración:** Vistas SQL optimizadas para Power BI

## Arquitectura de Solución

```
Google Cloud Storage (CSV Público)
         ↓
    Pandas Download
         ↓
BRONZE LAYER (Unity Catalog)
    Datos crudos - 2.38M registros
         ↓
SILVER LAYER (Unity Catalog)
    Limpieza + Enriquecimiento Temporal
         ↓
GOLD LAYER (Unity Catalog)
    KPIs, Zonas Críticas, Clasificación
         ↓
Vistas SQL Optimizadas
         ↓
Power BI (DirectQuery)
```

## Tecnologías Utilizadas

* **Databricks** - Plataforma de procesamiento
* **Apache Spark** - Motor de procesamiento distribuido
* **Unity Catalog** - Gobierno de datos
* **Delta Lake** - Almacenamiento ACID
* **Python** - Lenguaje principal
* **PySpark** - Procesamiento de Big Data
* **Power BI** - Visualización

## Sistema de Clasificación

| Nivel | Percentil | Prioridad | Presupuesto Sugerido |
|-------|-----------|-----------|----------------------|
| MUY CRÍTICA | ≥ 90 | 1 | 40% |
| CRÍTICA | 75-90 | 2 | 30% |
| ALTA | 50-75 | 3 | 20% |
| MEDIA | 25-50 | 4 | 8% |
| BAJA | < 25 | 5 | 2% |

## Tablas y Vistas Disponibles

### Tablas Gold en Unity Catalog

* `criminalidad.seguridad_ciudadana.bronze_delitos` - Datos crudos
* `criminalidad.seguridad_ciudadana.silver_delitos` - Datos limpios con enriquecimiento temporal
* `criminalidad.seguridad_ciudadana.gold_delitos_departamento` - Agregación por departamento
* `criminalidad.seguridad_ciudadana.gold_delitos_municipio` - Agregación por municipio
* `criminalidad.seguridad_ciudadana.gold_zonas_criticas` - Ranking de municipios
* `criminalidad.seguridad_ciudadana.gold_zonas_criticas_clasificadas` - Clasificación completa con niveles

### Vistas SQL para BI

* `v_dashboard` - Vista simplificada para dashboards ejecutivos
* `v_powerbi_zonas_criticas` - Vista optimizada con toda la información para Power BI

## Resultados Principales

### Top 5 Ciudades Más Críticas

1. **Bogotá D.C.** - 1,445,855 delitos
2. **Medellín** - 354,142 delitos
3. **Cali** - 291,408 delitos
4. **Barranquilla** - 133,931 delitos
5. **Cartagena** - 104,766 delitos

**Observación:** Las 5 ciudades principales concentran el 96.4% de la criminalidad registrada.

### Distribución de Criticidad

| Nivel | Municipios | Porcentaje |
|-------|------------|------------|
| MUY CRÍTICA | 112 | 10.08% |
| CRÍTICA | 165 | 14.85% |
| ALTA | 278 | 25.02% |
| MEDIA | 277 | 24.93% |
| BAJA | 279 | 25.11% |

## Ejecución del Proyecto

### Requisitos

* Workspace de Databricks con Unity Catalog
* Compute Serverless o cluster Databricks
* Acceso a Unity Catalog: `criminalidad.seguridad_ciudadana`

### Instrucciones

1. Abrir el notebook `Zonas_críticas_de_criminalidad_en_Colombia.ipynb`
2. Ejecutar todas las celdas secuencialmente (Run All)
3. Las tablas y vistas se crearán automáticamente en Unity Catalog
4. Conectar Power BI usando las vistas optimizadas

## Integración con Power BI

La vista recomendada para Power BI es: `criminalidad.seguridad_ciudadana.v_powerbi_zonas_criticas`

Esta vista incluye:
* Clasificación de criticidad
* Prioridades
* Recursos sugeridos
* Presupuesto relativo
* Ranking nacional
* Indicador de atención inmediata

## Autor

Alejandra Vargas (@alejabv4)

## Licencia

Este proyecto es de código abierto y está disponible bajo la licencia MIT.
