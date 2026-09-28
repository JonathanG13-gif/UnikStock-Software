# Casos de uso — UnikStock


## Los casos de uso del diagrama y los requisitos funcionales que realizan


**Actores:** Vendedor (encargado de mostrador) y Dueño/administrador.

| Caso de uso | Actor(es) | Requisitos funcionales que realiza |
|---|---|---|
| CU-01 Registrar venta | Vendedor | RF-001, RF-006 |
| CU-02 Registrar entrada de mercancía | Dueño/administrador | RF-002 |
| CU-03 Buscar producto | Vendedor y Dueño/administrador | RF-003 |
| CU-04 Consultar productos agotados | Vendedor y Dueño/administrador | RF-004 |
| CU-05 Registrar devolución | Vendedor | RF-005 |
| CU-06 Configurar nivel mínimo de stock | Dueño/administrador | RF-007 |
| CU-07 Consultar historial de ventas por día | Dueño/administrador | RF-008 |


---

## Caso de uso más importante, escrito completo


### CU-01 · Registrar venta

| Campo | Detalle |
|---|---|
| **Actor principal** | Vendedor |
| **Objetivo** | Cobrarle a un cliente los productos que se lleva y que el stock quede reflejado correctamente. |
| **Precondición** | El producto y su variante (talla/color/modelo) ya están dados de alta en el sistema. |

**Escenario principal**
1. El vendedor busca el producto por nombre o código.
2. El sistema muestra el producto con sus variantes y el stock disponible de cada una.
3. El vendedor selecciona la variante y la cantidad que el cliente se lleva.
4. El sistema verifica que hay suficiente stock de esa variante.
5. El sistema descuenta la cantidad vendida del stock de esa variante y registra la venta con la fecha.

**Flujos alternos**
- *1a. El producto no aparece en la búsqueda:* el sistema avisa que no encontró resultados, para que el vendedor revise el nombre o código, o avise al dueño si cree que falta darlo de alta.
- *4a. No hay suficiente stock de esa variante:* el sistema no permite continuar con esa cantidad y le muestra al vendedor cuánto hay disponible realmente.
- *4b. La variante ya está en cero:* el sistema le indica al vendedor que esa variante está agotada y, si existe, le sugiere revisar otra variante del mismo producto.

| Campo | Detalle |
|---|---|
| **Postcondición** | La venta queda registrada y el stock de la variante vendida queda actualizado. |
| **Requisitos que realiza** | RF-001, RF-006, RNF-USA-002, RNF-CON-001 |
