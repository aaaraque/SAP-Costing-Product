# SAP Product Costing (CO-PC) en SAP ERP 6.0 - Información Consolidada

Este documento consolida la información proporcionada sobre SAP Product Costing (CO-PC) en SAP ERP 6.0, enfocándose en los conceptos básicos, el Cálculo del Coste Estándar (CCE) y el flujo de costes a Órdenes de Fabricación.

---

## SAP Product Costing (CO-PC) in SAP ERP 6.0 - Overview

### 1. Purpose:
The primary goal of Product Costing is to calculate the Cost of Goods Manufactured (COGM) and Cost of Goods Sold (COGS). This information is crucial for:
*   **Inventory Valuation:** Determining the value of finished goods and work-in-process (WIP) inventory for financial statements.
*   **Pricing Decisions:** Providing a basis for setting sales prices.
*   **Profitability Analysis:** Understanding the profitability of different products.
*   **Cost Management:** Identifying cost drivers and areas for cost reduction.
*   **Make-or-Buy Decisions:** Comparing internal production costs with external procurement costs.

### 2. Key Components:
CO-PC isn't a single monolithic block but is composed of several integrated sub-components:

*   **Product Cost Planning (PCP):**
    *   **Focus:** Planning costs *before* actual production begins.
    *   **Main Tool:** Standard Cost Estimate. This calculates the planned cost of producing a material based on its Bill of Materials (BOM), Routing (sequence of operations), and planned prices/activity rates.
    *   **Usage:** Sets the standard cost for inventory valuation (if using standard costing), provides a benchmark for variance analysis, and can be used for preliminary profitability forecasts.
    *   **Key Objects:** Costing Variants (control *how* costing is done), Costing Sheets (apply overheads), Cost Component Structure (breakdown of costs like material, labor, overhead).

*   **Cost Object Controlling (COC):**
    *   **Focus:** Collecting actual costs incurred *during* the production process and comparing them against planned costs (target costs).
    *   **Cost Objects:** These are entities that incur costs, such as:
        *   **Production Orders / Process Orders:** For discrete or process manufacturing. Costs (material withdrawals, activity confirmations, overheads) are collected on these orders.
        *   **Product Cost Collectors:** Used in repetitive manufacturing scenarios.
        *   **Sales Orders:** Used in Make-to-Order scenarios where costs are tracked directly against a specific customer order.
    *   **Key Processes:** Simultaneous Costing (costs posted as they occur), Period-End Closing (WIP calculation, Variance Calculation, Settlement of order costs).

*   **Actual Costing / Material Ledger (ML):**
    *   **Focus:** Determining the *actual* costs of materials at the end of a period. While optional in ERP 6.0, it's highly recommended and often used.
    *   **Functionality:** Tracks material movements (goods receipts, invoices, production usage) at multiple valuations (e.g., legal, group, profit center). At period-end, it can revalue inventory and consumption based on calculated actual costs by rolling up price differences and production variances.
    *   **Benefit:** Provides a more accurate picture of actual inventory value and COGS, especially in environments with fluctuating prices or variances.

### 3. Integration:
CO-PC is tightly integrated with other SAP modules:

*   **Materials Management (MM):** Provides material master data, BOMs, material prices, goods movements.
*   **Production Planning (PP / PP-PI):** Provides Routings/Master Recipes, Work Centers/Resources, Production/Process Orders.
*   **Financial Accounting (FI):** Receives postings for inventory valuation, COGS, WIP, and production variances during settlement.
*   **Controlling (CO):** Uses Cost Centers (CO-OM-CCA) for overhead allocation, Activity Types for internal activity allocation (labor, machine time), and feeds results into Profitability Analysis (CO-PA).
*   **Sales and Distribution (SD):** Provides sales order information for make-to-order costing and profitability analysis.

### 4. Core Process Flow (Simplified):

*   **Planning Phase:**
    1.  Define Master Data (Materials, BOMs, Routings, Cost Centers, Activity Types, Prices/Rates).
    2.  Create Standard Cost Estimate for finished/semi-finished goods.
    3.  Mark and Release the Standard Cost Estimate (updates the material master standard price).
*   **Execution Phase (During the Period):**
    1.  Create Production/Process Orders.
    2.  Issue materials to the order (actual material costs collected).
    3.  Confirm activities (labor, machine time) against the order (actual activity costs collected).
    4.  Goods Receipt of finished product from the order (inventory valued at standard cost).
*   **Period-End Closing Phase:**
    1.  Calculate and apply Overhead costs to production orders (using Costing Sheets).
    2.  Calculate Work-in-Process (WIP) for open orders.
    3.  Calculate Variances (difference between target/standard costs and actual costs on the orders).
    4.  Settle Production Orders (post WIP and Variances to FI and potentially CO-PA).
    5.  (If Material Ledger is active) Execute ML closing cockpit to calculate actual costs and revalue inventory/consumption.

### 5. Key Concepts to Understand:

*   **Standard Cost:** A pre-determined, planned cost used for valuation and benchmarking.
*   **Actual Cost:** Costs actually incurred during production.
*   **Target Cost:** Costs that *should* have been incurred based on the actual quantity produced, valued at the standard rate.
*   **Variances:** Differences between actual costs and target/standard costs (e.g., price variance, quantity variance, resource-usage variance).
*   **Cost Component Structure:** A user-defined breakdown of costs (e.g., Raw Materials, Packaging, Direct Labor, Machine Overhead, Admin Overhead) providing visibility into the cost makeup.

---

## Cálculo del Coste del Producto (CO-PC) en SAP ERP 6.0 - Resumen (Español)

### 1. Propósito:
El objetivo principal del Cálculo del Coste del Producto es calcular el Coste de las Mercancías Fabricadas (COGM - Cost of Goods Manufactured) y el Coste de las Mercancías Vendidas (COGS - Cost of Goods Sold). Esta información es crucial para:
*   **Valoración de Inventarios:** Determinar el valor del inventario de productos terminados y trabajo en curso (WIP - Work in Process) para los estados financieros.
*   **Decisiones de Precios:** Proporcionar una base para establecer precios de venta.
*   **Análisis de Rentabilidad:** Comprender la rentabilidad de diferentes productos.
*   **Gestión de Costes:** Identificar los generadores de coste (cost drivers) y áreas para la reducción de costes.
*   **Decisiones de Fabricar o Comprar (Make-or-Buy):** Comparar los costes de producción interna con los costes de aprovisionamiento externo.

### 2. Componentes Clave:
CO-PC no es un único bloque monolítico, sino que se compone de varios subcomponentes integrados:

*   **Planificación de Costes del Producto (PCP):**
    *   **Enfoque:** Planificar los costes *antes* de que comience la producción real.
    *   **Herramienta Principal:** Cálculo del Coste Estándar. Calcula el coste planificado de producir un material basándose en su Lista de Materiales (**LMat / BOM**), Hoja de Ruta (**Routing** - secuencia de operaciones) y precios/tarifas de actividad planificados.
    *   **Uso:** Establece el coste estándar para la valoración de inventarios (si se utiliza el costeo estándar), proporciona un punto de referencia para el análisis de desviaciones y puede usarse para pronósticos preliminares de rentabilidad.
    *   **Objetos Clave:** Variantes de Cálculo del Coste (controlan *cómo* se realiza el cálculo del coste), Esquemas de Cálculo del Coste (aplican gastos generales), Estructura de Elementos de Coste (desglose de costes como material, mano de obra, gastos generales).

*   **Controlling de Objetos de Coste (COC):**
    *   **Enfoque:** Recopilar los costes reales incurridos *durante* el proceso de producción y compararlos con los costes planificados (costes teóricos).
    *   **Objetos de Coste:** Son entidades que incurren en costes, tales como:
        *   **Órdenes de Fabricación / Órdenes de Proceso:** Para fabricación discreta o por procesos. Los costes (salidas de material, notificaciones de actividad, gastos generales) se recopilan en estas órdenes.
        *   **Colectores de Costes del Producto:** Utilizados en escenarios de fabricación repetitiva.
        *   **Pedidos de Cliente:** Utilizados en escenarios de Fabricación sobre Pedido (Make-to-Order) donde los costes se rastrean directamente contra un pedido de cliente específico.
    *   **Procesos Clave:** Cálculo del Coste Simultanéo (costes contabilizados a medida que ocurren), Cierre del Periodo (cálculo de WIP/Trabajo en Curso, Cálculo de Desviaciones, Liquidación de los costes de la orden).

*   **Cálculo del Coste Real / Ledger de Materiales (ML):**
    *   **Enfoque:** Determinar los costes *reales* de los materiales al final de un período. Aunque es opcional en ERP 6.0, es muy recomendable y se usa a menudo.
    *   **Funcionalidad:** Rastrea los movimientos de material (entradas de mercancías, facturas, consumos de producción) en múltiples valoraciones (p. ej., legal, de grupo, de centro de beneficio). Al cierre del período, puede revalorizar el inventario y el consumo basándose en los costes reales calculados, distribuyendo las diferencias de precio y las desviaciones de producción.
    *   **Beneficio:** Proporciona una imagen más precisa del valor real del inventario y del COGS, especialmente en entornos con precios fluctuantes o desviaciones.

### 3. Integración:
CO-PC está estrechamente integrado con otros módulos de SAP:

*   **Gestión de Materiales (MM):** Proporciona datos maestros de material, Listas de Materiales (LMat), precios de material, movimientos de mercancías.
*   **Planificación de la Producción (PP / PP-PI):** Proporciona Hojas de Ruta/Recetas de Planificación, Puestos de Trabajo/Recursos, Órdenes de Fabricación/Proceso.
*   **Gestión Financiera (FI):** Recibe contabilizaciones para la valoración de inventarios, COGS, WIP/Trabajo en Curso y desviaciones de producción durante la liquidación.
*   **Controlling (CO):** Utiliza Centros de Coste (CO-OM-CCA) para la imputación de gastos generales, Clases de Actividad para la asignación de actividad interna (mano de obra, tiempo de máquina) y alimenta los resultados al Análisis de Rentabilidad (CO-PA).
*   **Ventas y Distribución (SD):** Proporciona información de pedidos de cliente para el cálculo del coste para pedido de cliente y el análisis de rentabilidad.

### 4. Flujo del Proceso Central (Simplificado):

*   **Fase de Planificación:**
    1.  Definir Datos Maestros (Materiales, LMat, Hojas de Ruta, Centros de Coste, Clases de Actividad, Precios/Tarifas).
    2.  Crear el Cálculo del Coste Estándar para productos terminados/semielaborados.
    3.  Marcar y Liberar el Cálculo del Coste Estándar (actualiza el precio estándar en el maestro de materiales).
*   **Fase de Ejecución (Durante el Período):**
    1.  Crear Órdenes de Fabricación/Proceso.
    2.  Emitir materiales a la orden (costes reales de material recopilados).
    3.  Notificar actividades (mano de obra, tiempo de máquina) contra la orden (costes reales de actividad recopilados).
    4.  Entrada de Mercancías del producto terminado desde la orden (inventario valorado a coste estándar).
*   **Fase de Cierre del Período:**
    1.  Calcular y aplicar costes de Gastos Generales a las órdenes de producción (usando Esquemas de Cálculo del Coste).
    2.  Calcular el Trabajo en Curso (**TEC/WIP**) para órdenes abiertas.
    3.  Calcular Desviaciones (diferencia entre costes teóricos/estándar y costes reales en las órdenes).
    4.  Liquidar Órdenes de Fabricación (contabilizar WIP y Desviaciones en FI y potencialmente en CO-PA).
    5.  (Si el Ledger de Materiales está activo) Ejecutar el cockpit de cierre de ML para calcular los costes reales y revalorizar inventario/consumo.

### 5. Conceptos Clave a Entender:

*   **Coste Estándar:** Un coste predeterminado y planificado utilizado para valoración y como punto de referencia.
*   **Coste Real:** Costes realmente incurridos durante la producción.
*   **Coste Teórico:** Costes que *deberían* haberse incurrido según la cantidad real producida, valorada a la tarifa estándar.
*   **Desviaciones:** Diferencias entre los costes reales y los costes teóricos/estándar (p. ej., desviación de precio, desviación de cantidad, desviación de empleo de recursos).
*   **Estructura de Elementos de Coste:** Un desglose definido por el usuario de los costes (p. ej., Materias Primas, Embalaje, Mano de Obra Directa, Gastos Generales de Máquina, Gastos Generales de Administración) que proporciona visibilidad sobre la composición del coste.

---

## Pilar 1: El Cálculo del Coste Estándar (CCE) - Desglose Detallado (Español)

El CCE es la piedra angular de la planificación de costes y la valoración en muchos entornos.

### Objetivo Profundo
No es solo un número, es una *declaración estructurada* de cómo se espera formar el coste de un producto bajo condiciones *normales* o *planificadas*. Busca establecer un valor estable y predecible.

### Componentes de Entrada (Los "Ingredientes" del Coste)

*   **Estructura Cuantitativa (¿Qué y Cómo se Hace?):**
    *   **Lista de Materiales (LMat / BOM):**
        *   **Detalle:** Especifica la *cantidad exacta* de componentes necesaria por unidad base (considerando desperdicios).
        *   **Relevancia:** Usa la LMat válida en la fecha clave y componentes marcados como relevantes.
        *   **Recursividad:** Calcula costes de semielaborados primero si son componentes (costeo multinivel).
        *   **Transacciones Clave:** `CS01`/`CS02`/`CS03`.
    *   **Hoja de Ruta (Routing) / Receta de Planificación (Master Recipe):**
        *   **Detalle:** Define operaciones, Puesto de Trabajo/Recurso (vinculado a Centro de Coste y Clases de Actividad), y cantidades de actividad planificadas (Valores Prefijados). La Clave de Control indica relevancia para coste.
        *   **Relevancia:** Selecciona la Hoja de Ruta/Receta válida según cantidad y fecha.
        *   **Transacciones Clave:** `CA01`/`02`/`03`, `C201`/`02`/`03`.

*   **Valoración (¿Cuánto Cuesta?):**
    *   **Precios de Material:**
        *   **Fuente:** Maestro de Materiales (Vistas Contabilidad 1 / Cálculo de Coste 1).
        *   **Estrategia:** Definida en la Variante de Cálculo de Coste (prioridad: Precio Estándar, Precio Medio Variable, Precio Planificado, etc.).
        *   **Impacto:** Elección del precio del componente afecta resultado y análisis de desviaciones.
        *   **Transacciones Clave:** `MM03`.
    *   **Tarifas de Actividad:**
        *   **Fuente:** Planificadas en Contabilidad de Centros de Coste (`CO-CCA`) por Centro de Coste / Clase de Actividad.
        *   **Cálculo:** Tarifa = Costes Planificados CC / Cantidad Actividad Planificada CC.
        *   **Vinculación:** Puesto de Trabajo enlaza operación con CC/Clase Actividad para encontrar la tarifa.
        *   **Transacciones Clave:** `KP26`.
    *   **Gastos Generales (Overheads):**
        *   **Mecanismo:** Usando un **Esquema de Cálculo del Coste (Costing Sheet)**.
        *   **Estructura del Esquema:** Define *Base* (sobre qué costes directos aplicar), *Tasa de Recargo* (% o cantidad fija), y *Abono* (objeto que absorbe el coste).
        *   **Flexibilidad:** Permite aplicar diferentes tipos de gastos generales.
        *   **Transacciones Clave:** `KZS2`.

### Proceso de Cálculo (La "Cocina")

*   **Ejecución:** Transacciones `CK11N` (individual) o `CK40N` (masiva - Costing Run).
*   **Pasos Internos:**
    1.  **Determinación Estructura Cuantitativa:** Lee LMat y Hoja de Ruta/Receta.
    2.  **Valoración:** Multiplica cantidades de material por precios, cantidades de actividad por tarifas, y aplica recargos de gastos generales.
    3.  **Agregación y Estructuración:** Suma costes y los desglosa según la **Estructura de Elementos de Coste (Cost Component Structure - CCS)** (`OKTZ`).

### Resultado Detallado
*   Coste total planificado por unidad.
*   Desglose por elemento de coste (visión CCS).
*   Log detallado (ítemización) del cálculo.

### Pasos Posteriores Cruciales
*   **Análisis:** Revisión de resultados (`CK13N`).
*   **Marcado (Marking):** (`CK24`) Autoriza el CCE. Guarda resultado como precio estándar *futuro* en el maestro de materiales.
*   **Liberación (Release):** (`CK24` o `CK40N`) Activa el CCE marcado. Copia precio estándar futuro al *actual*. **Este precio se usa para valorar entradas y consumos (si control precio 'S')**.

---

## Pilar 2: Flujo Básico de Costes Hacia una Orden de Fabricación - Desglose Detallado (Español)

La Orden de Fabricación/Proceso es donde el plan (CCE) se encuentra con la realidad.

### Creación de la Orden (`CO01`/`COR1`)
*   Se crea para un material y cantidad específicos.
*   Puede calcular *costes planificados* iniciales basados en CCE y cantidad.
*   Se convierte en un **colector de costes** individual.

### Flujo de Costes Reales (Débitos a la Orden)

1.  **Consumo de Materiales (Salida de Mercancías - `MIGO`, Mov 261):**
    *   **Evento:** Entrega física de componentes desde almacén.
    *   **Registro SAP:** Salida con referencia a la Orden.
    *   **Valoración Detallada:** Cantidad *real* consumida * Precio *actual* del componente (Estándar si 'S', MAP si 'V').
    *   **Contabilización:**
        *   *Débito:* Cuenta Gasto Consumo (P&L) con Orden como objeto CO -> Aumenta coste *real* orden.
        *   *Crédito:* Cuenta Inventario Componente (Balance) -> Disminuye inventario.

2.  **Consumo de Actividades (Notificación - `CO11N`/`COR6N`):**
    *   **Evento:** Realización de trabajo (operarios, máquinas).
    *   **Registro SAP:** Notificación de cantidades *reales* de actividad (horas, etc.) para la operación/orden.
    *   **Valoración Detallada:** Cantidad *real* notificada * *Tarifa planificada* (de `KP26`). (Puede revalorizarse con Coste Real/ML).
    *   **Contabilización:**
        *   *Débito:* Cuenta Gasto Secundaria (CO) con Orden como objeto CO -> Aumenta coste *real* orden.
        *   *Crédito:* Centro de Coste / Clase de Actividad -> Descarga el centro de coste.

3.  **Aplicación de Gastos Generales (Ejecución Recargo - `CO43`, `KGI2`):**
    *   **Evento:** Proceso periódico (usualmente mensual) para asignar indirectos.
    *   **Registro SAP:** Transacción aplica tasas del Esquema de Cálculo de Coste sobre bases reales acumuladas.
    *   **Valoración Detallada:** Tasas (% o fija) aplicadas sobre costes *reales* base en la orden.
    *   **Contabilización:**
        *   *Débito:* Cuenta Gasto con Orden como objeto CO -> Aumenta coste *real* orden.
        *   *Crédito:* Centro de Coste de Abono (del Esquema) -> Simula absorción gasto general.

### Descarga de la Orden (Crédito a la Orden)

1.  **Entrada de Producto Terminado (Entrada de Mercancías - `MIGO`, Mov 101):**
    *   **Evento:** Finalización y entrada a almacén del producto fabricado.
    *   **Registro SAP:** Entrada de mercancías desde la Orden.
    *   **Valoración CRÍTICA:** Cantidad *real* producida valorada SIEMPRE al **Precio Estándar** del producto terminado (del CCE liberado).
    *   **Contabilización:**
        *   *Débito:* Cuenta Inventario Producto Terminado (Balance) -> Aumenta inventario al estándar.
        *   *Crédito:* Cuenta "Variación de existencias" (P&L) con Orden como objeto CO -> **Reduce (abona) saldo orden por valor estándar producido.**

### El Estado Intermedio
*   La Orden tiene:
    *   **Total Débitos:** Costes reales acumulados.
    *   **Total Créditos:** Valor estándar de la producción real entregada.
*   El **Saldo de la Orden** (Débitos - Créditos) es la diferencia preliminar Real vs. Estándar.

### El Siguiente Paso (Cierre del Periodo - un Vistazo)
El saldo de la orden se analiza y liquida al final del periodo:
*   **Determinación de Trabajo en Curso (WIP):** Si la orden está abierta, se calcula y capitaliza el valor de la producción no terminada.
*   **Cálculo de Desviaciones:** Si la orden está terminada (o para la parte terminada), el saldo restante se clasifica en categorías de desviación (precio, cantidad, eficiencia, etc.).
*   **Liquidación:** El saldo final (WIP o Desviaciones) se transfiere de la orden a FI (cuentas WIP, Desviaciones) y/o CO-PA. La orden queda saldada.

---
**Fin del Documento Consolidado**
