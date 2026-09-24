# Especificación de requisitos — UnikStock

> Este documento cubre el entregable **2. Especificación de requisitos** de la evaluación parcial. Cada sección trae una etiqueta con lo que cubre del checklist.

---

## 1. Propósito y alcance

> ✅ Cubre: "Propósito y alcance, retomado de la Visión del producto."
> (Ya lo tenía escrito, se copia tal cual de la Visión del producto de la Unidad 1.)

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

> ✅ Cubre: "Usuarios y su contexto, enriquecido con lo que salió de la entrevista."
> (La tabla base ya la tenía; lo que agrego aquí es lo que confirmé en la entrevista, marcado abajo.)

| Usuario | Qué hace hoy sin el sistema | Qué espera del sistema |
|---|---|---|
| Dueño/administrador (yo) | Revisa físicamente el perchero/vitrina o lleva cuentas sueltas en libreta | Ver el inventario completo por categoría, registrar mercancía nueva, ver qué se vendió y qué se está agotando, sin que capturar un producto nuevo sea tedioso |
| Vendedor de medio tiempo | Revisa físicamente si hay talla/color disponible antes de vender | Registrar una venta rápido y confirmar disponibilidad de talla/color sin ir a revisar físicamente, sin llenar muchos campos con el cliente esperando |

**Lo que confirmé en la entrevista (nuevo respecto a la Visión del producto):**
- Solo el dueño y un vendedor de medio tiempo usan el sistema; nadie más. El vendedor vende pero no decide qué se reabastece.
- Cuando llega un pedido grande de un proveedor y hay clientes en el mostrador al mismo tiempo, la entrada de mercancía se anota primero en papel y se captura después, lo que a veces genera errores u omisiones. Por eso el registro de entrada de mercancía debe ser rápido de llenar (ver RNF de usabilidad).

**Tensión entre usuarios:** más detalle por variante ayuda a mi control como dueño, pero puede hacer más lenta la venta en mostrador para el vendedor. Los requisitos de usabilidad de abajo intentan no resolver esto del todo, sino dejarlo balanceado.

---

## 3. Requisitos funcionales

> ✅ Cubre: "Requisitos funcionales con ficha completa: descripción, origen, prioridad, criterio de aceptación y relaciones."
> (La redacción de cada requisito ya la tenía de la sesión anterior; lo nuevo aquí es la ficha completa por requisito — Origen, Prioridad y Relaciones — que es lo que pide la actividad.)

**RF-001 — Descontar stock al vender**
- Descripción: El sistema debe descontar del stock la cantidad exacta vendida al confirmarse una venta, por variante específica (talla/color/modelo), no de forma general por producto.
- Origen: Visión del producto, confirmado en la entrevista.
- Prioridad: Alta.
- Criterio de aceptación: al registrar una venta de una variante, el stock de esa variante baja exactamente en la cantidad vendida y ninguna otra variante se ve afectada.
- Relaciona con: CU-01 Registrar venta.

**RF-002 — Registrar entrada de mercancía**
- Descripción: El sistema debe permitir registrar la entrada de nueva mercancía al inventario, especificando categoría, variante, cantidad y fecha.
- Origen: Visión del producto, confirmado y enriquecido en la entrevista (ver punto de la libreta/papel en la sección de usuarios).
- Prioridad: Alta.
- Criterio de aceptación: se puede dar de alta una entrada de mercancía nueva o sumarla a una variante existente, y el stock de esa variante queda actualizado de inmediato.
- Relaciona con: CU-02 Registrar entrada de mercancía.

**RF-003 — Buscar producto por nombre o código**
- Descripción: El sistema debe permitir buscar un producto por nombre o código.
- Origen: Visión del producto.
- Prioridad: Alta.
- Criterio de aceptación: al escribir parte del nombre o el código de un producto, aparece en la lista de resultados junto con sus variantes disponibles.
- Relaciona con: CU-03 Buscar producto.

**RF-004 — Mostrar productos agotados**
- Descripción: El sistema debe mostrar el producto en una lista visible de "agotados" dentro del panel en cuanto el stock de esa variante llegue a cero.
- Origen: Visión del producto.
- Prioridad: Media.
- Criterio de aceptación: en cuanto una variante llega a cero unidades, aparece en la lista de agotados sin que nadie tenga que revisarlo manualmente.
- Relaciona con: CU-04 Consultar productos agotados.

**RF-005 — Registrar devolución**
- Descripción: El sistema debe permitir registrar una devolución y reintegrar la cantidad devuelta al stock de la variante correspondiente.
- Origen: Visión del producto.
- Prioridad: Media.
- Criterio de aceptación: al registrar una devolución de una variante, el stock de esa variante sube exactamente en la cantidad devuelta.
- Relaciona con: CU-05 Registrar devolución.

**RF-006 — Rechazar venta que deje stock en negativo**
- Descripción: El sistema debe rechazar el registro de una venta si esta deja el stock de la variante en un valor negativo.
- Origen: Visión del producto.
- Prioridad: Alta.
- Criterio de aceptación: si se intenta vender más piezas de una variante de las que hay en stock, el sistema no registra la venta y avisa que no hay suficiente stock.
- Relaciona con: CU-01 Registrar venta (flujo alterno).

**RF-007 — Configurar nivel mínimo de stock por variante**
- Descripción: El sistema debe permitir configurar un nivel mínimo de stock distinto por producto o variante, no un mínimo único global.
- Origen: Visión del producto.
- Prioridad: Media.
- Criterio de aceptación: puedo asignar un mínimo distinto a cada variante (por ejemplo, 1 para un reloj de edición limitada y 5 para una gorra básica) y el sistema respeta ese número al generar alertas.
- Relaciona con: CU-06 Configurar nivel mínimo de stock.

**RF-008 — Mostrar historial de ventas por día**
- Descripción: El sistema debe mostrar el historial de ventas agrupado por día.
- Origen: Visión del producto.
- Prioridad: Baja.
- Criterio de aceptación: puedo elegir un día y ver la lista de ventas registradas ese día, con producto, variante y cantidad.
- Relaciona con: CU-07 Consultar historial de ventas por día.

---

## 4. Requisitos no funcionales

> ✅ Cubre: "Requisitos no funcionales agrupados por atributo de calidad, cada uno con su métrica."
> (Ya tenía identificados los atributos y la redacción; lo que faltaba y agrego ahora son los números concretos, usando lo que salió en la entrevista — catálogo de ~150 productos y máximo 2 usuarios al mismo tiempo.)

**Usabilidad** — importa porque se usa en mostrador, entre cliente y cliente, con productos de categorías muy distintas que hay que capturar rápido.
- RNF-001: Registrar un producto nuevo no debe requerir más de 5 campos obligatorios por categoría.
- RNF-002: Registrar una venta en mostrador no debe tomar más de 3 pasos desde que se busca el producto hasta que se confirma.

**Consistencia de datos** — importa porque el stock que se muestra tiene que ser el que realmente hay en el estante.
- RNF-003: El stock mostrado no debe divergir del stock real en más de 1 unidad, incluso ante ventas simultáneas.

**Disponibilidad** — importa porque se necesita todos los días de operación de la tienda.
- RNF-004: El sistema debe estar disponible de 10:00 a 20:00, los días que la tienda opera.

**Desempeño** — importa para no hacer esperar al cliente en el mostrador.
- RNF-005: Una consulta o búsqueda de producto debe responder en menos de 5 segundos, con un catálogo de hasta 150 productos y hasta 2 usuarios conectados al mismo tiempo (el dueño y el vendedor).

**Flexibilidad de datos** — importa porque cada categoría tiene su propia variante (talla en ropa, modelo en relojes, color en gorras y collares).
- RNF-006: El sistema debe soportar que cada categoría de producto tenga su propio tipo de variante, sin obligar a las demás categorías a usar el mismo campo.

---

## 5. Tabla de trazabilidad

> ✅ Cubre: "Tabla de trazabilidad y registro de cambios."

| Requisito | Caso de uso que lo realiza |
|---|---|
| RF-001 | CU-01 Registrar venta |
| RF-002 | CU-02 Registrar entrada de mercancía |
| RF-003 | CU-03 Buscar producto |
| RF-004 | CU-04 Consultar productos agotados |
| RF-005 | CU-05 Registrar devolución |
| RF-006 | CU-01 Registrar venta (flujo alterno) |
| RF-007 | CU-06 Configurar nivel mínimo de stock |
| RF-008 | CU-07 Consultar historial de ventas por día |

Todos los requisitos funcionales quedan cubiertos por al menos un caso de uso, y ningún caso de uso queda sin un requisito detrás.

## 6. Registro de cambios

| Versión | Qué cambió |
|---|---|
| 1.0 | Primera versión: propósito, alcance, tipo de sistema y requisitos iniciales (Visión del producto). |
| 1.1 | Se agregaron los requisitos no funcionales agrupados por atributo, con los valores numéricos aún pendientes. |
| 1.2 | Después de la entrevista: se llenaron los valores numéricos de los requisitos no funcionales, se agregó el campo Origen y Prioridad a cada requisito funcional, se quitó de raíz la idea de contemplar multi-sucursal, y se agregó la tabla de trazabilidad. |

---

## 7. Revisión de la dupla

> ⚠️ Pendiente de completar por ti: esta sección la tienes que llenar con tu dupla real, porque es un requisito para que el trabajo se pueda evaluar. Aquí solo dejo el espacio con el formato listo.

- Nombre de mi dupla: ______
- Fecha de revisión: ______
- Comentarios recibidos: ______
- Cambios que hice a partir de esa revisión: ______
