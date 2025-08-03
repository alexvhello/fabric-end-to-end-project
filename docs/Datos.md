# 📂 Estructura de Datos y Modelado

Este proyecto utiliza la **arquitectura medallón** (Bronze, Silver, Gold) para gobernanza y calidad de datos, y finaliza en un **modelo semántico optimizado** para Power BI bajo un **esquema copo de nieve (snowflake)**.

---

## 🏗 Diseño de Capas

### **1. Bronze (Datos Crudos)**
- **Propósito:** Almacenar los datos tal como provienen de los orígenes (SQL Server y SharePoint).
- **Ejemplo de tablas:**
  - `ContratosRaw`
  - `ClientesRaw`
  - `ClasificacionesRaw`
- **Características:**
  - Sin transformaciones.
  - Datos usados para trazabilidad y auditoría.

---

### **2. Silver (Transformación y Calidad)**
- **Propósito:** Limpieza, normalización y enriquecimiento.
- **Procesos:**
  - Tipificación de datos.
  - Eliminación de duplicados.
  - Creación de **llaves subrogantes (SK)**.
- **Ejemplo de tablas:**
  - `ClientesSilver` (con SK_Cliente)
  - `ClasificacionesSilver`
  - `FactContratosSilver` (enlaza SK de dimensiones)

---

### **3. Gold (Modelo Semántico en Warehouse)**
El **modelo semántico final** utiliza un **esquema copo de nieve**, integrando dimensiones principales y jerárquicas.

#### 📐 Diagrama del Modelo
![Modelo Semántico](/assets/diagramas/modelo-semantico.png)

#### ✅ Tablas Principales y Función

---

#### **Tabla de Hechos**
- **factContratos**
  - Contiene información detallada de contratos y métricas financieras.
  - Campos clave:
    - `montoCompraFinal`, `fechaAprobacion`, `fechaCancelacion`.
    - Llaves foráneas hacia dimensiones (SK).

---

#### **Dimensiones Principales**
- **dimClientes**
  - Información de clientes con referencias jerárquicas:
    - `skCanal`
    - `skIndustria`
    - `skSegmentoComercial`
    - `skValorEstrategico`
  - Atributos: `fechaIngreso`, `nombreCliente`.

- **dimActivos**
  - Información de activos y categorías.
  - Campos: `descripcionActivo`, `skCategoriaActivo`.

---

#### **Dimensiones Jerárquicas (Snowflake)**
- **dimCanal**
  - Detalle de canales de adquisición (ej.: Directo, Tercero, Call Center).
- **dimIndustria**
  - Clasificación por sector (ej.: Construcción, Gobierno).
- **dimSegmentoComercial**
  - Segmentos como Institucional, PyME, Gobierno, etc.
- **dimValorEstrategico**
  - Valor estratégico asignado al cliente (Alto, Medio, Bajo).
- **dimCategoria**
  - Clasificación de activos por categoría.

---

#### **Dimensión de Tiempo**
- **dimDate**
  - Tabla calendario para análisis temporal.
  - Campos: `Año`, `Mes`, `Trimestre`, `Día`.

Código DAX para su creación:
```DAX
Calendario =
ADDCOLUMNS (
    CALENDAR (DATE(2020; 01; 01); DATE(2030; 12; 31));
    "Año"; YEAR([Date]);
    "Mes"; FORMAT([Date]; "MMMM");
    "MesNum"; MONTH([Date]);
    "Trimestre"; "T" & FORMAT(QUARTER([Date]); "0");
    "Semana"; WEEKNUM([Date]);
    "Dia"; DAY([Date])
)
