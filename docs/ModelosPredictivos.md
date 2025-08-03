# 🤖 Modelos Predictivos en Microsoft Fabric y Azure ML

Este proyecto incluye **dos modelos predictivos principales**, diseñados para agregar valor al análisis descriptivo en Power BI:

---

## ✅ 1. Modelo de Churn (Cancelación Anticipada)

**Objetivo:**  
Predecir la **probabilidad de cancelación** de un contrato antes de que ocurra, permitiendo acciones preventivas.

### 📐 **Flujo de Trabajo**
- **Fuente de datos:**  
  Tablas de la **capa Silver**, enriquecidas con:
  - Datos del cliente.
  - Historial de contratos.
  - Montos de compra.
  - Variables derivadas (antigüedad, uso, clasificación).
- **EDA (Exploratory Data Analysis):**  
  Notebook `notebookEDA` analiza correlaciones, valores faltantes y variables relevantes.
- **Entrenamiento:**  
  - Implementado en **Azure ML** y cuadernos en **Fabric**.
  - Modelos probados: **Logistic Regression**, **Random Forest**, **XGBoost**.
  - **Mejor modelo:** XGBoost con ajuste de hiperparámetros.
- **Evaluación:**
  - **Métrica principal:** AUC = **0.91**.
  - **Precisión:** 89%.
- **Pipeline en Azure ML:**  
  Automatiza:
  - Ingesta → Preprocesamiento → Entrenamiento → Registro en MLflow.
- **Scoring:**  
  Realizado en el notebook `notebookChurnScoring`.  
  Los resultados se cargan en la **capa Gold** para consumo en Power BI.

---

## ✅ 2. Modelo de Segmentación de Clientes (Clustering)

**Objetivo:**  
Agrupar clientes en segmentos homogéneos para **estrategias comerciales personalizadas**.

### 📐 **Flujo de Trabajo**
- **Fuente de datos:**  
  Tablas de clientes (Silver) con variables:
  - Monto total histórico.
  - Frecuencia de compra.
  - Duración del contrato.
  - Clasificación por industria y segmento.
- **EDA:**  
  Identificación de outliers y normalización de datos.
- **Entrenamiento:**  
  - Algoritmo: **K-Means**.
  - Número de clústeres: **4** (determinado por método del codo y silhouette score).
- **Interpretación:**  
  - Segmento 0: Clientes institucionales con compras altas.
  - Segmento 1: Clientes PyME con frecuencia media.
  - Segmento 2: Clientes gobierno con compras puntuales.
  - Segmento 3: Clientes individuales con bajo ticket.
- **Resultados:**  
  Tabla `PrediccionesSegmentacion` en la **capa Gold**.
- **Scoring:**  
  Realizado en `notebookClusteringScoring` y almacenado para su visualización.

---

## ✅ Integración en Power BI
Los resultados de ambos modelos se integran en el **modelo semántico de Power BI** para:
- Mostrar **probabilidad de churn por contrato**.
- Visualizar **segmentos de clientes** en informes descriptivos y predictivos.

---

## 📊 Ejemplo en Dashboard
![Predicciones en Power BI](/assets/capturas/informe-contratos-2.png)

**Visualizaciones:**
- Tabla con **predicciones de churn** y probabilidad.
- Análisis mensual con comportamiento y activadores.
- Clústeres asignados por cliente en la segunda tabla.

---

## ✅ Beneficios del Enfoque
- **Prevención del churn** → Acciones tempranas para clientes en riesgo.
- **Estrategia comercial segmentada** → Marketing dirigido según clústeres.
- **Escalabilidad** → Nuevos modelos pueden integrarse en la misma arquitectura.
