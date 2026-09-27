# Casos de uso — UnikStock (documentación completa)

> Los 7 casos de uso documentados con la misma estructura de la plantilla del curso: Actor principal, Objetivo, Precondición, Escenario principal, Flujos alternos, Postcondición y Requisitos que realiza.

---

## CU-01 · Registrar venta

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
- *4a. No hay suficiente stock de esa variante:* el sistema no permite continuar con esa cantidad y le muestra al vendedor cuánto hay disponible realmente.
- *4b. La variante ya está en cero:* el sistema le indica al vendedor que esa variante está agotada y, si existe, le sugiere revisar otra variante del mismo producto.
- *1a. El producto no aparece en la búsqueda:* el sistema avisa que no encontró resultados, para que el vendedor revise el nombre o código, o avise al dueño si cree que falta darlo de alta.

| Campo | Detalle |
|---|---|
| **Postcondición** | La venta queda registrada y el stock de la variante vendida queda actualizado. |
| **Requisitos que realiza** | RF-001, RF-006, RF-003 |

---

## CU-02 · Registrar entrada de mercancía

| Campo | Detalle |
|---|---|
| **Actor principal** | Dueño / administrador |
| **Objetivo** | Sumar al inventario la mercancía nueva que llega de un proveedor, para que el stock quede al día. |
| **Precondición** | El producto ya existe en el catálogo, o se va a dar de alta en este mismo momento. |

**Escenario principal**
1. El dueño busca el producto al que le va a agregar mercancía, o inicia el alta de uno nuevo.
2. El sistema muestra las variantes existentes de ese producto (o un formulario vacío si es nuevo).
3. El dueño indica la variante (talla/color/modelo), la cantidad que llegó y la fecha.
4. El sistema suma la cantidad al stock de esa variante.
5. El sistema confirma que la entrada quedó registrada.

**Flujos alternos**
- *2a. El producto no existe todavía:* el dueño lo da de alta con categoría, nombre y su primera variante, y continúa el registro de entrada.
- *3a. La variante indicada no existe para ese producto:* el sistema permite crear la variante nueva en el mismo paso.

| Campo | Detalle |
|---|---|
| **Postcondición** | El stock de la variante queda actualizado con la cantidad que llegó, y la entrada queda registrada con su fecha. |
| **Requisitos que realiza** | RF-002 |

---

## CU-03 · Buscar producto

| Campo | Detalle |
|---|---|
| **Actor principal** | Vendedor (también lo usa el Dueño / administrador) |
| **Objetivo** | Encontrar un producto y ver de inmediato qué variantes tiene disponibles. |
| **Precondición** | El producto está dado de alta en el sistema. |

**Escenario principal**
1. La persona escribe parte del nombre o el código del producto.
2. El sistema busca coincidencias conforme se va escribiendo.
3. El sistema muestra la lista de productos que coinciden.
4. La persona selecciona el producto que buscaba.
5. El sistema muestra sus variantes y el stock disponible de cada una.

**Flujos alternos**
- *3a. No hay coincidencias:* el sistema avisa que no encontró resultados, para que la persona revise el nombre o el código.

| Campo | Detalle |
|---|---|
| **Postcondición** | La persona sabe con certeza qué variantes hay disponibles de ese producto, sin ir físicamente al estante. |
| **Requisitos que realiza** | RF-003 |

---

## CU-04 · Consultar productos agotados

| Campo | Detalle |
|---|---|
| **Actor principal** | Dueño / administrador (también lo usa el Vendedor) |
| **Objetivo** | Ver de un vistazo qué variantes ya no tienen stock, para saber qué reabastecer o qué explicarle a un cliente. |
| **Precondición** | Ninguna, aparte de que el sistema ya tenga productos registrados. |

**Escenario principal**
1. La persona abre la sección de "Agotados".
2. El sistema muestra la lista de todas las variantes que están en cero unidades.
3. La persona identifica qué necesita reabastecer, o le explica al cliente por qué no hay esa variante.

**Flujos alternos**
- *2a. No hay ninguna variante agotada:* el sistema muestra la lista vacía con un mensaje de que todo tiene stock por ahora.

| Campo | Detalle |
|---|---|
| **Postcondición** | La persona tiene a la mano, sin revisar el estante, la lista actualizada de lo que ya no hay. |
| **Requisitos que realiza** | RF-004 |

---

## CU-05 · Registrar devolución

| Campo | Detalle |
|---|---|
| **Actor principal** | Vendedor |
| **Objetivo** | Reintegrar al stock un producto que un cliente devuelve, dejando registro de esa devolución. |
| **Precondición** | La venta original de esa variante ya está registrada en el sistema. |

**Escenario principal**
1. El vendedor busca la venta original o el producto que se está devolviendo.
2. El sistema muestra la variante y la cantidad que se vendió.
3. El vendedor indica cuántas piezas se devuelven.
4. El sistema reintegra esa cantidad al stock de la variante.
5. El sistema confirma que la devolución quedó registrada.

**Flujos alternos**
- *1a. No se encuentra la venta original:* el vendedor registra la devolución indicando manualmente el producto y la variante, sin ligarla a una venta específica.
- *3a. La cantidad devuelta es mayor a la vendida:* el sistema no permite continuar y le pide al vendedor revisar la cantidad.

| Campo | Detalle |
|---|---|
| **Postcondición** | El stock de la variante devuelta queda actualizado con las piezas reintegradas. |
| **Requisitos que realiza** | RF-005 |

---

## CU-06 · Configurar nivel mínimo de stock

| Campo | Detalle |
|---|---|
| **Actor principal** | Dueño / administrador |
| **Objetivo** | Definir a partir de cuántas piezas una variante se considera "por agotarse", para que el aviso de stock bajo tenga sentido según cada producto. |
| **Precondición** | El producto y su variante ya están dados de alta. |

**Escenario principal**
1. El dueño entra a la variante que quiere configurar.
2. El sistema muestra el nivel mínimo actual (si ya tenía uno).
3. El dueño indica el nuevo nivel mínimo para esa variante.
4. El sistema guarda el nuevo valor y lo aplica desde ese momento.

**Flujos alternos**
- *3a. El dueño deja el campo vacío o en cero:* el sistema usa un mínimo por defecto y le avisa al dueño qué valor quedó aplicado.

| Campo | Detalle |
|---|---|
| **Postcondición** | Esa variante usa su propio nivel mínimo al momento de generar alertas de stock bajo. |
| **Requisitos que realiza** | RF-007 |

---

## CU-07 · Consultar historial de ventas por día

| Campo | Detalle |
|---|---|
| **Actor principal** | Dueño / administrador |
| **Objetivo** | Revisar qué se vendió en un día específico, para llevar control del negocio. |
| **Precondición** | Debe haber al menos una venta registrada. |

**Escenario principal**
1. El dueño abre la sección de historial de ventas.
2. El dueño elige el día que quiere revisar.
3. El sistema muestra la lista de ventas de ese día, con producto, variante y cantidad.

**Flujos alternos**
- *3a. No hubo ventas ese día:* el sistema muestra la lista vacía con un mensaje indicando que no hubo movimientos.

| Campo | Detalle |
|---|---|
| **Postcondición** | El dueño conoce el detalle de lo vendido ese día sin tener que revisar la libreta. |
| **Requisitos que realiza** | RF-008 |
