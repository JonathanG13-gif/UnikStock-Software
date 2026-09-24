# Casos de uso — UnikStock (detalle escrito)



## Lista de casos de uso (5 a 8, como pide la actividad)

> "Identifica los actores... Lista entre cinco y ocho casos de uso."

**Actores:** Vendedor (encargado de mostrador), Dueño/administrador.

1. Registrar venta
2. Buscar producto
3. Registrar devolución
4. Consultar productos agotados
5. Registrar entrada de mercancía
6. Configurar nivel mínimo de stock
7. Consultar historial de ventas por día

Prueba de cada nombre: al terminar cualquiera de estos, la persona (vendedor o dueño) se puede ir satisfecha con algo resuelto, no a medias.

---

## CU-01 · Registrar venta

> "Escribe completo el caso de uso más importante de tu sistema, con escenario principal y al menos dos flujos alternos" + "anota qué requisitos funcionales realiza."

Elegí este caso de uso porque es el que más se usa en el día a día y el que junta la mayoría de las reglas de negocio del sistema (descuento de stock, validación de que no quede en negativo).

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
- **4a. No hay suficiente stock de esa variante:** el sistema no permite continuar con esa cantidad y le muestra al vendedor cuánto hay disponible realmente, para que ajuste la cantidad o revise si hay otra variante.
- **4b. La variante ya está en cero:** el sistema le indica al vendedor que esa variante está agotada y, si existe, le sugiere revisar otra variante del mismo producto (por ejemplo otra talla).
- **1a. El producto no aparece en la búsqueda:** el sistema le avisa al vendedor que no encontró resultados, para que revise el nombre o código, o le avise al dueño si cree que falta darlo de alta.

**Postcondición:** la venta queda registrada y el stock de la variante vendida queda actualizado.

**Requisitos que realiza:** RF-001, RF-006 (rechazo de stock negativo), RF-003 (para la búsqueda del paso 1).
