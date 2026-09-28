# Especificación de requisitos — UnikStock


---

## 1. Propósito y alcance


**Propósito:** Este documento define qué debe hacer UnikStock y bajo qué condiciones, para que me sirva de referencia mientras lo construyo y como criterio para saber si ya quedó bien. Va dirigido a mí mismo, porque soy el desarrollador y el dueño del negocio (Unik Syle) al mismo tiempo.

**Dentro del alcance:**
- Registro de productos por categoría (ropa, relojes, collares, gorras) con nombre, categoría, variante (talla/color/modelo), precio y cantidad en stock.
- Registro de ventas con descuento automático de stock por variante.
- Alerta visual cuando una variante baja de su nivel mínimo.
- Historial de ventas por día.

**Fuera del alcance:**
- Facturación electrónica / CFDI.
- Cobro con tarjeta integrado (pasarela de pago).
- Tienda en línea con carrito de compras.
- Multi-sucursal (control de más de una tienda a la vez).
- Reportes contables o de impuestos.

---

## 2. Usuarios y su contexto

| Usuario | Qué hace hoy sin el sistema | Qué espera del sistema |
|---|---|---|
| Dueño/administrador (yo) | Revisa físicamente el perchero/vitrina o lleva cuentas sueltas en libreta | Ver el inventario completo por categoría, registrar mercancía nueva, ver qué se vendió y qué se está agotando, sin que capturar un producto nuevo sea tedioso |
| Vendedor de medio tiempo | Revisa físicamente si hay talla/color disponible antes de vender | Registrar una venta rápido y confirmar disponibilidad de talla/color sin ir a revisar físicamente, sin llenar muchos campos con el cliente esperando |

**Lo que confirmé en la entrevista (nuevo respecto a la Visión del producto):**
- Solo el dueño y un vendedor de medio tiempo usan el sistema; nadie más. El vendedor vende pero no decide qué se reabastece.
- Cuando llega un pedido grande de un proveedor y hay clientes en el mostrador al mismo tiempo, la entrada de mercancía se anota primero en papel y se captura después, lo que a veces genera errores u omisiones. Por eso el registro de entrada de mercancía debe ser rápido de llenar (ver RNF de usabilidad).

**Tensión entre usuarios:** más detalle por variante ayuda a mi control como dueño/socio, pero puede hacer más lenta la venta en mostrador para el vendedor. Los requisitos de usabilidad de abajo intentan no resolver esto del todo, sino dejarlo balanceado.

---

## 3. Requisitos funcionales


**RF-001 — Descontar stock al vender**
- Descripción: El sistema debe descontar del stock la cantidad exacta vendida al confirmarse una venta, por variante específica (talla/color/modelo), no de forma general por producto.
- Origen: Visión del producto. **Confirmado** en la entrevista: la libreta casi nunca cuadra con lo que hay en el estante.
- Prioridad: Alta.
- Criterio de aceptación: al registrar una venta de una variante, el stock de esa variante baja exactamente en la cantidad vendida y ninguna otra variante se ve afectada.
- Relaciones: CU-01 Registrar venta; RF-006; RNF-CON-001.

**RF-002 — Registrar entrada de mercancía**
- Descripción: El sistema debe permitir registrar la entrada de nueva mercancía al inventario, especificando categoría, variante, cantidad y fecha.
- Origen: Visión del producto. **Confirmado** en la entrevista: la mercancía nueva se anota primero en papel y se captura después.
- Prioridad: Alta.
- Criterio de aceptación: al registrar una entrada con variante, cantidad y fecha, el stock de esa variante sube exactamente en esa cantidad y la entrada queda guardada con su fecha.
- Relaciones: CU-02 Registrar entrada de mercancía; RNF-USA-001.

**RF-003 — Buscar producto por nombre o código**
- Descripción: El sistema debe permitir buscar un producto por nombre o código.
- Origen: Visión del producto. **Confirmado** en la entrevista: cuando un cliente pregunta por una talla o color hay que ir al estante a revisar.
- Prioridad: Alta.
- Criterio de aceptación: al escribir parte del nombre o el código de un producto, aparece en la lista de resultados junto con sus variantes disponibles.
- Relaciones: CU-03 Buscar producto; RNF-REN-001.

**RF-004 — Mostrar productos agotados**
- Descripción: El sistema debe mostrar el producto en una lista visible de "agotados" dentro del panel en cuanto el stock de esa variante llegue a cero.
- Origen: Visión del producto. **Supuesto**, no salió directamente en la entrevista.
- Prioridad: Media.
- Criterio de aceptación: al abrir la lista de agotados justo después de la venta que dejó una variante en cero, esa variante ya aparece ahí sin haberla agregado a mano.
- Relaciones: CU-04 Consultar productos agotados; RF-007.

**RF-005 — Registrar devolución**
- Descripción: El sistema debe permitir registrar una devolución y reintegrar la cantidad devuelta al stock de la variante correspondiente.
- Origen: Visión del producto. **Supuesto**, no salió directamente en la entrevista.
- Prioridad: Media.
- Criterio de aceptación: al registrar una devolución de una variante, el stock de esa variante sube exactamente en la cantidad devuelta.
- Relaciones: CU-05 Registrar devolución; RF-001.

**RF-006 — Rechazar venta que deje stock en negativo**
- Descripción: El sistema debe rechazar el registro de una venta si esta deja el stock de la variante en un valor negativo.
- Origen: Visión del producto (regla de negocio que ya había identificado). **Supuesto**, no salió directamente en la entrevista.
- Prioridad: Alta.
- Criterio de aceptación: si se intenta vender más piezas de una variante de las que hay en stock, el sistema no registra la venta y avisa que no hay suficiente stock.
- Relaciones: CU-01 Registrar venta (flujo alterno); RF-001.

**RF-007 — Configurar nivel mínimo de stock por variante**
- Descripción: El sistema debe permitir configurar un nivel mínimo de stock distinto por producto o variante, no un mínimo único global.
- Origen: Visión del producto (regla de negocio que ya había identificado). **Supuesto**, no salió directamente en la entrevista.
- Prioridad: Media.
- Criterio de aceptación: puedo asignar un mínimo distinto a cada variante (por ejemplo, 1 para un reloj de edición limitada y 5 para una gorra básica) y el sistema respeta ese número al generar alertas.
- Relaciones: CU-06 Configurar nivel mínimo de stock; RF-004.

**RF-008 — Mostrar historial de ventas por día**
- Descripción: El sistema debe mostrar el historial de ventas agrupado por día.
- Origen: Visión del producto. **Supuesto**, no salió directamente en la entrevista.
- Prioridad: Baja.
- Criterio de aceptación: puedo elegir un día y ver la lista de ventas registradas ese día, con producto, variante y cantidad.
- Relaciones: CU-07 Consultar historial de ventas por día; RF-001.

---

## 4. Requisitos no funcionales


**Usabilidad** — importa porque se usa en mostrador, entre cliente y cliente, con productos de categorías muy distintas que hay que capturar rápido.
- RNF-USA-001: Registrar un producto nuevo no debe requerir más de 5 campos obligatorios por categoría.
  - Métrica: máximo 5 campos obligatorios.
  - Por qué ese límite: son justo los datos del alcance (nombre, categoría, variante, precio y cantidad); si pide más, la mercancía se me sigue quedando en el papel.
- RNF-USA-002: Registrar una venta en mostrador no debe tomar más de 3 pasos desde que se busca el producto hasta que se confirma.
  - Métrica: máximo 3 pasos.
  - Por qué ese límite: buscar, elegir variante y cantidad, y confirmar; el vendedor atiende con el cliente esperando.

**Consistencia de datos** — importa porque el stock que se muestra tiene que ser el que realmente hay en el estante.
- RNF-CON-001: El stock mostrado no debe divergir del stock real en más de 1 unidad, incluso ante ventas simultáneas.
  - Métrica: diferencia máxima de 1 unidad.
  - Por qué ese límite: hay piezas de edición limitada con mínimo de 1 unidad; una diferencia mayor podría hacerme vender algo que ya no existe.

**Disponibilidad** — importa porque se necesita todos los días de operación de la tienda.
- RNF-DIS-001: El sistema debe estar disponible de 10:00 a 20:00, los días que la tienda opera.
  - Métrica: disponible durante todo el horario de 10:00 a 20:00.
  - Por qué ese límite: la tienda abre a las diez y ese es el horario en que se atiende y se registran ventas.

**Desempeño** — importa para no hacer esperar al cliente en el mostrador.
- RNF-REN-001: Una consulta o búsqueda de producto debe responder en menos de 5 segundos, con un catálogo de hasta 150 productos y hasta 2 usuarios conectados al mismo tiempo (el dueño y el vendedor).
  - Métrica: menos de 5 segundos.
  - Por qué ese límite: hoy el cliente espera varios minutos mientras reviso el estante; 5 segundos ya es una mejora enorme y no lo hace esperar en caja.

**Flexibilidad de datos** — importa porque cada categoría tiene su propia variante (talla en ropa, modelo en relojes, color en gorras y collares).
- RNF-FLE-001: El sistema debe permitir que cada categoría de producto tenga su propio tipo de variante, sin obligar a las demás categorías a usar el mismo campo.
  - Métrica: 4 de 4 categorías (ropa, relojes, collares, gorras) se registran con su propio tipo de variante, sin campos que no les apliquen.
  - Por qué ese límite: un reloj no tiene talla pero una playera sí.

---

## 5. Casos de uso

| Caso de uso | Actor principal |
|---|---|
| CU-01 Registrar venta | Vendedor |
| CU-02 Registrar entrada de mercancía | Dueño/administrador |
| CU-03 Buscar producto | Vendedor (también el dueño) |
| CU-04 Consultar productos agotados | Dueño/administrador (también el vendedor) |
| CU-05 Registrar devolución | Vendedor |
| CU-06 Configurar nivel mínimo de stock | Dueño/administrador |
| CU-07 Consultar historial de ventas por día | Dueño/administrador |

---

## 6. Trazabilidad y control de cambios


### Tabla de trazabilidad

| Requisito | De dónde salió | Caso de uso que lo realiza |
|---|---|---|
| RF-001 | Visión del producto; confirmado en la entrevista | CU-01 Registrar venta |
| RF-002 | Visión del producto; confirmado en la entrevista | CU-02 Registrar entrada de mercancía |
| RF-003 | Visión del producto; confirmado en la entrevista | CU-03 Buscar producto |
| RF-004 | Visión del producto; supuesto | CU-04 Consultar productos agotados |
| RF-005 | Visión del producto; supuesto | CU-05 Registrar devolución |
| RF-006 | Visión del producto; supuesto | CU-01 Registrar venta (flujo alterno) |
| RF-007 | Visión del producto; supuesto | CU-06 Configurar nivel mínimo de stock |
| RF-008 | Visión del producto; supuesto | CU-07 Consultar historial de ventas por día |
| RNF-USA-001 | Visión del producto (usabilidad); confirmado con lo del papel en la entrevista | CU-02 |
| RNF-USA-002 | Visión del producto (usabilidad) | CU-01 |
| RNF-CON-001 | Reglas de negocio de la Visión del producto | CU-01, CU-02, CU-05 |
| RNF-DIS-001 | Entrevista (la tienda abre a las diez) | Todos |
| RNF-REN-001 | Entrevista (catálogo de ~150 productos y 2 usuarios) | CU-03 |
| RNF-FLE-001 | Visión del producto (flexibilidad de datos) | CU-02 |


### Registro de cambios

| Versión | Qué cambió |
|---|---|
| 1.0 | Primera versión: propósito, alcance, tipo de sistema y requisitos iniciales (Visión del producto). |
| 1.1 | Se agregaron los requisitos no funcionales agrupados por atributo, con los valores numéricos aún pendientes. |
| 1.2 | Después de la entrevista: se llenaron los valores numéricos de los requisitos no funcionales, se agregó el campo Origen y Prioridad a cada requisito funcional, se confirmó que lo de multi-sucursal no aplica y sigue fuera del alcance. |
| 1.3 | Tras validar el documento contra la plantilla: el campo Origen ahora distingue lo confirmado de lo supuesto; se agregaron las relaciones entre requisitos; se aclararon los criterios de aceptación de RF-002 y RF-004; los requisitos no funcionales pasaron a la nomenclatura con código de atributo (por ejemplo RNF-REN-001),


---

## 7. Revisión de la dupla

- Nombre de mi dupla: Ian Adolfo Lopez
- Fecha de revisión: 
- Comentarios recibidos:
  - El criterio de aceptación de RF-002 mezclaba dos cosas (dar de alta y sumar) y decía "de inmediato" sin medirlo.
  - El criterio de RF-004 tampoco decía qué tan rápido debía aparecer el producto en la lista de agotados.
  - RNF-FLE-001 no tenía nada que medir.
- Cambios que hice a partir de esa revisión: reescribí los criterios de RF-002 y RF-004, le puse métrica a RNF-FLE-001 (4 de 4 categorías) y marqué en Origen cada requisito como confirmado o supuesto.
