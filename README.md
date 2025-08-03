# 🚀 Microsoft Fabric End-to-End Project

![Microsoft Fabric](https://img.shields.io/badge/Microsoft%20Fabric-Analytics%20Platform-purple)
![Status](https://img.shields.io/badge/status-active-brightgreen)
![PowerBI](https://img.shields.io/badge/Power%20BI-DAX-yellow)
![AzureML](https://img.shields.io/badge/Azure%20Machine%20Learning-ML-blue)

End-to-end project integrating **Microsoft Fabric**, **Power BI**, and **Machine Learning**.  
Includes **data ingestion, medallion architecture (Bronze, Silver, Gold), ETL pipelines, semantic modeling, dashboards, and predictive models**.

---

## 📌 **Contenido**
| Sección | Descripción |
|---------|-------------|
| [🖥 Arquitectura](docs/Arquitectura.md) | Diseño medallón (Bronze, Silver, Gold) y flujo general |
| [📂 Datos](docs/Datos.md) | Capas, tablas, claves sustitutas (SK), calendario |
| [🔄 ETL](docs/ETL.md) | Dataflows Gen2, Pipelines, procesos automáticos |
| [📊 Power BI](docs/PowerBI.md) | Dashboards, KPIs y medidas DAX |
| [🤖 Modelos Predictivos](docs/ModelosPredictivos.md) | Churn, predicción de abonos, segmentación |
| [⚙ Deployment](docs/Deployment.md) | Cómo implementar y mantener el proyecto |
| [📈 Monitoreo](docs/Monitoreo.md) | Supervisión de recursos y capacidades en Fabric |

---

## 🏗 **Arquitectura del Proyecto**
El diseño sigue el enfoque **Medallion Architecture**:
- **Bronze:** Ingesta de datos desde SQL Server y SharePoint
- **Silver:** Transformaciones y limpieza en Lakehouse
- **Gold:** Modelado semántico en Warehouse para Power BI

### 📐 **Diagrama**
![Arquitectura](assets/diagramas/arquitectura.jpg)

---

## 🔄 **Flujo de Tareas**
Basado en los flujos nativos de Microsoft Fabric:

![Flujo de Tareas](assets/diagramas/taskflow.png)

- **Obtener datos:** Extracción desde orígenes on-premise y cloud
- **Tienda:** Lakehouse (Bronze, Silver)
- **Preparar:** Transformaciones y curación de datos
- **Análisis y Entrenamiento:** Modelos ML en Azure ML + Notebooks
- **Visualizar:** Dashboards en Power BI
- **Distribuir:** Publicación y consumo por usuarios
- **Seguimiento:** Monitoreo del rendimiento y métricas

---

## 🛠 **Tecnologías Utilizadas**
- **Microsoft Fabric**: Lakehouse, Warehouse, Pipelines, Dataflows Gen2
- **Power BI**: KPIs, informes, dashboards
- **Azure Machine Learning**: Entrenamiento, scoring y despliegue
- **SQL Server / SharePoint**: Orígenes de datos
- **GitHub**: Control de versiones y documentación

---

## ▶ **Cómo Ejecutar**
1. Clona este repositorio:
   ```bash
   git clone https://github.com/alexvhello/fabric-end-to-end-project.git
