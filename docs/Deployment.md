# ⚙ Deployment del Proyecto en Microsoft Fabric

Este documento describe los pasos para **implementar el proyecto completo en un nuevo entorno**, asegurando que se cumpla la arquitectura medallón, los procesos ETL, los modelos predictivos y la visualización en Power BI.

---

## ✅ 1. Requisitos Previos

- **Licencias y Servicios:**
  - Microsoft Fabric habilitado (SKU dependerade varios factores, entre ellos, operaciones interactivas y en segundo plano).
  - Power BI Pro o Premium (licencias de paga en caso de que el SKU de Fabric sea menos a F64).
  - Azure Machine Learning Workspace.
- **Roles:**
  - **Miembro** o superior en el Workspace de Fabric.
  - Permisos para crear elementos como lakehouses, warehouses y pipelines.
- **Herramientas:**
  - Power BI Desktop.
  - Git.

---

## ✅ 2. Clonar el Repositorio

```bash
git clone https://github.com/alexvhello/fabric-end-to-end-project.git
cd fabric-end-to-end-project
