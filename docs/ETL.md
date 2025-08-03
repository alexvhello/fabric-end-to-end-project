# 🔄 Procesos ETL (Extract, Transform, Load)

Este documento detalla los procesos de **ingesta, transformación y carga** implementados en el proyecto, siguiendo el enfoque de **arquitectura medallón**.

---

## 🏗 Arquitectura de Capas (3 capas)
- **Bronze:** Datos crudos, tal como provienen de las fuentes.
- **Silver:** Datos limpios, normalizados y con reglas de negocio aplicadas.
- **Gold:** Datos listos para análisis, organizados en un modelo semántico.

---

## ✅ 1. Capa Bronze (Ingesta)

La capa **Bronze** recibe los datos **en su forma original** desde diferentes orígenes. Aquí **no se realizan transformaciones**, solo almacenamiento.

### 🔹 Orígenes y Procesos
- **SQL Server (On-Premise):**
  - **pipelineTablas:** Orquesta la carga de contratos y tablas relacionadas desde SQL Server hacia el **lakehouseBronze**.
- **SharePoint:**
  - **dataflowCanal:** Carga datos de canales de distribución.
  - **dataflowIndustria:** Carga datos de clasificación por industria.
  - **dataflowSegmentoComercial:** Carga datos por segmento comercial.
  - **dataflowValorEstrategico:** Carga datos de clasificación por valor estratégico.
- **Archivos en Lakehouse:**
  - **notebookClientesBronze:** Integra archivos de clientes en formato CSV/Parquet a tablas dentro de la capa Bronze.

### 🔍 Objetivo:
- Mantener **datos crudos para trazabilidad y auditoría**.
- Soportar diferentes formatos: CSV, Parquet, Delta.

---

## ✅ 2. Capa Silver (Transformación)

En esta capa se realiza la **limpieza, tipificación, normalización y aplicación de reglas de negocio**.  
Aquí se incorporan las **llaves subrogantes (SK)** y se crean tablas intermedias para modelado y análisis.

### 🔹 Dataflows Gen2
- **dataflowClasificaciones:** Transforma tablas de clasificación de clientes.
- **dataflowClientes:** Limpia y estandariza la tabla de clientes.
- **dataflowProject:** Procesa la tabla de contratos y datos asociados.

### 🔹 Notebooks en Fabric
- **notebookMoneda:** Genera tabla de moneda.
- **notebookEjecutivoGrupoActivo:** Prepara tablas de ejecutivos, grupos y activos.
- **notebookEjecutivoGrupoSilver:** Agrega llaves subrogantes a ejecutivos y grupos.
- **notebookActivoSilver:** Llaves subrogantes en activos.
- **notebookCategoriaSilver:** Llaves subrogantes en categorías.
- **notebookClasificaciones:** Llaves subrogantes en clasificaciones de clientes.
- **notebookClientesSilver:** Llaves subrogantes en clientes.
- **notebookFactContratosSilver:** Llaves subrogantes en contratos.

### 🔍 Objetivo:
- Garantizar **consistencia y calidad de datos**.
- Preparar datasets para **modelos predictivos** y análisis BI.

---

## ✅ 3. Capa Gold (Modelado y Consumo)

Aquí los datos se consolidan en el **Warehouse** bajo un **esquema estrella** para maximizar el rendimiento en Power BI y soportar el modelo semántico.

### 🔹 Dataflows
- **dataflowDimClientes:** Carga dimensión clientes a Gold.
- **dataflowDimEjeGrupo:** Carga dimensiones de ejecutivos y grupos.
- **dataflowDimClasificaciones:** Carga clasificaciones finales.
- **dataflowPredictions:** Integra resultados de modelos predictivos (Churn y Segmentación).

### 🔍 Objetivo:
- Optimizar consultas para **Power BI DirectLake**.
- Integrar resultados analíticos con modelos predictivos.

---

## ✅ 4. Orquestación y Automatización

### 🔹 Pipelines en Fabric
- **pipelineTablas:** Ingesta desde SQL Server.
- **pipelinesDatasets:** Generación de datasets para modelos ML.

### 🔹 Integración con Machine Learning
- Modelos entrenados (Churn y Segmentación) generan predicciones que se integran en Gold mediante **dataflowPredictions**.

---

## ✅ 5. Beneficios del ETL en Fabric
- **Unificación:** Proceso centralizado en Fabric (Dataflows, Notebooks, Pipelines) mediante OneLake.
- **Escalabilidad:** Compatible con grandes volúmenes gracias a Delta Lake.
- **Automatización:** Pipelines programados y disparadores para ejecución continua.
