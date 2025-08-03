# 📈 Monitoreo y Administración en Microsoft Fabric

El monitoreo es un componente esencial para garantizar el **rendimiento, gobernanza y control de costos** en entornos Microsoft Fabric.  
Este proyecto está preparado para aprovechar las capacidades nativas de **Microsoft Fabric Capacity Metrics**.

---

## ✅ ¿Qué es Fabric Capacity Metrics?
Es un conjunto de herramientas integradas en el **admin portal de Fabric** que permite:
- Visualizar **uso de recursos** (memoria, CPU, almacenamiento).
- Identificar **picos de consumo y procesos intensivos**.
- Configurar **alertas y notificaciones** sobre límites.
- Optimizar cargas y asignación de capacidades en tiempo real.

---

## ✅ Diagrama de Monitoreo en el Flujo
![Monitoreo en Fabric](/assets/diagramas/monitoreo-fabric.png)

En este proyecto, el monitoreo se encuentra al final del pipeline, supervisando:
- Ejecución de Dataflows y Pipelines.
- Cargas en Lakehouse y Warehouse.
- Conexiones de Power BI (DirectLake).
- Notebooks y procesos de Machine Learning.

---

## ✅ Áreas que se monitorean en este proyecto
1. **Pipelines y Dataflows**
   - Seguimiento de ejecuciones, duración y errores.
   - Control de **refresh programados**.
2. **Lakehouse y Warehouse**
   - Uso de almacenamiento en **OneLake**.
   - Consultas más costosas y su impacto en la capacidad.
3. **Modelos Semánticos (Power BI)**
   - Consumo de memoria por datasets conectados vía **DirectLake**.
4. **Notebooks y ML**
   - Ejecuciones de notebooks.
   - Costos asociados a experimentos y scoring.

---

## ✅ Cómo acceder

Para supervisar el uso de recursos y capacidades en Microsoft Fabric, sigue estos pasos:

### 1. Instalar la aplicación **Capacity Metrics**
- Accede a **Microsoft Fabric → Centro de administración**.
- Dirígete a **Capacidades**.
- Haz clic en **Obtener aplicación de métricas (Capacity Metrics App)**.
- Instala la aplicación en tu organización.

### 2. Abrir la aplicación y acceder al informe
- Una vez instalada, la aplicación aparecerá en **Aplicaciones → Capacity Metrics**.
- Ábrela y selecciona el **informe principal**.

### 3. Seleccionar la capacidad a monitorear
- Dentro del informe, en el panel lateral, ubica el **selector de capacidad**.
- Elige la capacidad asignada al proyecto (ejemplo: *SKU F4*).

### 4. Revisar y configurar
- Analiza:
   - **Uso actual y tendencias** de CPU, memoria y almacenamiento.
   - **Historial de consumo** por día o por proceso.
- Configura **alertas personalizadas** desde:
   - **Microsoft 365 Admin Center** o **Azure Monitor** para recibir notificaciones proactivas.

---

## ✅ Beneficios
- **Prevención de cuellos de botella**: Detecta procesos pesados antes de afectar el rendimiento.
- **Optimización de costos**: Ajusta la asignación de SKU según demanda.
- **Gobernanza y trazabilidad**: Garantiza que los recursos se utilicen de forma eficiente y controlada.

---

📌 Más información oficial:  
[Documentación de Monitoreo en Microsoft Fabric](https://learn.microsoft.com/es-es/fabric/enterprise/metrics-app)
