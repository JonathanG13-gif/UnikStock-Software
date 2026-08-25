# Visión del producto

> **Plantilla del curso · Ingeniería de Software I · SIS3407**
> Este documento es el primer entregable del semestre y la base de todo lo que viene después.
> Se entrega completo en la **semana 4** y se presenta ante el grupo.
>
> **Cómo usarla:** copia este archivo a tu repositorio como `docs/vision-del-producto.md`, borra las instrucciones en gris de cada apartado y escribe tu contenido en su lugar. Conserva los títulos.

---

**Autor: Jonathan Michel García Pacheco**
**Fecha de la última versión: 18/08/2026**
**Repositorio: Proyecto Ing Software 1**

---

## 1. Descripción del sistema

*Instrucción: nombre del sistema y qué hace, en un párrafo que cualquier persona entienda sin ser del área. Si necesitas usar una palabra técnica para explicarlo, todavía no está listo.*

**Nombre del sistema: Unik Stock**

**Descripción: UnikStock es un sistema que ayuda al dueño de una tienda de ropa y accesorios a saber en todo momento qué productos tiene disponibles, en qué tallas o variantes, y cuáles se están agotando. En lugar de recordar de memoria o revisar físicamente el estante cada vez que llega un cliente, el dueño consulta el sistema desde su celular o computadora y sabe al instante qué hay y qué falta reabastecer.
**

---

## 2. Problema y usuarios

*Instrucción: qué problema resuelve, a quién le sirve y, muy importante, qué hace esa gente hoy para arreglárselas sin el sistema. Esa última parte es la que revela el problema real.*

**El problema: Cuando una tienda maneja productos muy distintos entre sí (ropa con tallas, relojes con modelos, collares y gorras con variantes de color), es fácil perder el control de cuánto queda de cada cosa, vender algo que ya no existe en esa talla o color, o descubrir que un producto se agotó hasta que un cliente lo pide.
**

**Cómo se resuelve hoy sin el sistema:**

**Usuarios del sistema: Revisando físicamente el perchero o la vitrina, o llevando cuentas sueltas en el celular o una libreta, lo cual se vuelve poco confiable cuando hay muchas categorías de producto con variantes distintas cada una (talla en ropa, color en gorras, modelo en relojes).
**

| Tipo de usuario | Qué necesita del sistema | Qué le preocupa |
|---|---|---|
|Dueño/administrador |Ver el inventario completo por categoría, registrar mercancía nueva, ver qué se vendió y qué se está agotando |Que capturar un producto nuevo no sea tedioso, dado que cada categoría tiene datos distintos (talla vs. modelo vs. color) |
|Vendedor/encargado de mostrador |Registrar una venta rápido y saber si hay una talla o color disponible sin ir a revisar físicamente |Que el sistema no lo obligue a llenar muchos campos cuando el cliente ya está esperando en caja |

*Instrucción: necesitas al menos dos tipos de usuario con necesidades distintas. Si los dos quieren exactamente lo mismo, probablemente sean el mismo usuario.*

**Un conflicto entre usuarios: El dueño quiere que cada producto tenga toda su variante bien especificada (talla, color, modelo) para saber exactamente qué reabastecer, pero el vendedor quiere vender rápido sin tener que buscar entre muchas opciones parecidas. Más detalle en el catálogo ayuda al control, pero puede hacer más lenta la venta en mostrador.**

*Instrucción: describe algo que un usuario quiera y que a otro le estorbe. Ahí está tu primera decisión de diseño real.*

---

## 3. Alcance

*Instrucción: lo que escribes en "fuera del alcance" es lo que después evita que el proyecto crezca sin control. Sé específico: "reportes" no dice nada, "reportes de ventas mensuales exportables a PDF" sí.*

Cinco cosas que el sistema sí hace (verbos verificables)

Registra cada producto nuevo con su categoría, variante (talla, color o modelo) y precio.

Descuenta automáticamente el stock de la variante correspondiente cuando se captura una venta.

Muestra la cantidad disponible de cada variante de producto en tiempo real.

Marca visualmente (por ejemplo con un color de alerta) cualquier variante cuyo stock caiga por debajo del mínimo definido para ella.

Lista el historial de ventas realizadas en un día o rango de fechas específico.


Tres cosas que el sistema explícitamente no hace

No cobra ni procesa pagos con tarjeta o transferencia.

No genera facturas electrónicas (CFDI).

No publica un catálogo en línea donde los clientes puedan comprar directamente.

### Dentro del alcance

-
-
-
-

### Explícitamente fuera del alcance

-
-
-

**Por qué queda fuera:**

*Instrucción: para al menos una de las exclusiones, explica la razón. Puede ser tiempo, complejidad, o que no aporta al problema central.*

---

## 4. Tipo de sistema y restricciones

*Instrucción: identifica de qué tipo es tu sistema y qué te obliga a garantizar ese tipo. Un sistema de información y un sistema crítico no se diseñan igual.*

**Tipo de sistema:**

*(De información · Embebido · Crítico · Web y SaaS · De datos y análisis)*

**Por qué es de ese tipo:**

**Atributos de calidad que impone:**

| Atributo | Por qué importa en mi caso | Qué pasa si no se cumple |
|---|---|---|
| | | |
| | | |
| | | |

**Reglas de negocio que ya identifiqué:**

*Instrucción: reglas que no son obvias desde fuera y que alguien que conoce el dominio tendría que explicarte. Si no encuentras ninguna, tu caso puede ser demasiado simple.*

1.
2.
3.

---

## 5. Ciclo de vida elegido

*Instrucción: este apartado se trabaja en la semana 3, después de ver los modelos de desarrollo. La justificación pesa más que la elección: no hay un modelo correcto, hay uno defendible para tu caso.*

**Modelo elegido:**

**Por qué le conviene a este proyecto:**

*Instrucción: argumenta con las características reales de tu caso. Estabilidad de los requisitos, disponibilidad del cliente, nivel de riesgo, tamaño del equipo, frecuencia de entregas esperada.*

### Alternativas descartadas

**Alternativa 1:**

*Por qué la descarté:*

**Alternativa 2:**

*Por qué la descarté:*

---

## Antes de entregar

Reviso que el documento cumpla lo siguiente:

- [ ] La descripción del apartado 1 se entiende sin ser del área
- [ ] Hay al menos dos tipos de usuario con necesidades distintas
- [ ] Identifiqué un conflicto real entre usuarios
- [ ] El alcance dice qué queda fuera, no solo qué queda dentro
- [ ] Las exclusiones son específicas, no genéricas
- [ ] Identifiqué el tipo de sistema y al menos dos atributos de calidad
- [ ] Anoté al menos tres reglas de negocio no obvias
- [ ] Justifiqué el ciclo de vida contra dos alternativas descartadas
- [ ] El documento está en mi repositorio y se puede leer desde el navegador
- [ ] Borré todas las instrucciones en cursiva de la plantilla
