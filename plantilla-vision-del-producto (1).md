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

**Un conflicto entre usuarios: Los vendedores por querer vender rapido se les olvida o como tal no registran la venta haciendo que el inventario en el sistema se mueva y el dueño tenga los datos de manera incorrecta.**

*Instrucción: describe algo que un usuario quiera y que a otro le estorbe. Ahí está tu primera decisión de diseño real.*

---

## 3. Alcance

*Instrucción: lo que escribes en "fuera del alcance" es lo que después evita que el proyecto crezca sin control. Sé específico: "reportes" no dice nada, "reportes de ventas mensuales exportables a PDF" sí.*

###Cinco cosas que el sistema sí hace (verbos verificables)

Registra cada producto nuevo con su categoría, variante (talla, color o modelo) y precio.

Descuenta automáticamente el stock de la variante correspondiente cuando se captura una venta.

Muestra la cantidad disponible de cada variante de producto en tiempo real.

Marca visualmente (por ejemplo con un color de alerta) cualquier variante cuyo stock caiga por debajo del mínimo definido para ella.

Lista el historial de ventas realizadas en un día o rango de fechas específico.




###Tres cosas que el sistema explícitamente no hace

No genera una pagina web para clientes.

No genera facturas electrónicas.

No publica un catálogo en línea donde los clientes puedan comprar directamente.


###Razón de una exclusión

No genera facturas electrónicas porque eso requiere conectarse a un proveedor certificado por el SAT y cumplir reglas fiscales específicas — es un proyecto de integración aparte que no aporta al problema central, que es simplemente saber qué hay en existencia y qué se ha vendido.

###Funcionalidad futura (no requisito de este semestre)

Me encantaría que el sistema sugiera combinaciones de productos (por ejemplo, "quien compró esta gorra también suele llevar este collar") para ayudar a vender más por cliente, casi como una recomendación automática de outfit según el estilo. Es una idea de valor agregado interesante, pero implica análisis de datos históricos de venta que no cabe en el alcance de este semestre — queda anotada como idea futura, no como requisito.


**Dentro del alcance**

- Registro de productos por categoría (ropa, relojes, collares, gorras) con nombre, categoría, variante (talla/color/modelo), precio y cantidad en stock
- Registro de ventas (descuenta del stock automáticamente según la variante vendida)
- Alerta visual cuando una variante de producto baja de cierto nivel mínimo
- Vista de historial de ventas por día

**Explícitamente fuera del alcance**

- Facturación electrónica
- Tienda en línea con carrito de compras
- Reportes contables o de impuestos

**Por qué queda fuera:**

*Instrucción: para al menos una de las exclusiones, explica la razón. Puede ser tiempo, complejidad, o que no aporta al problema central.*

 La tienda en línea con carrito de compras implica manejo de pagos, envíos y catálogo público, lo cual es un proyecto completo aparte; el objetivo aquí es únicamente resolver el control de inventario de la tienda física, no crear un canal de venta nuevo.


## 4. Tipo de sistema y restricciones

*Instrucción: identifica de qué tipo es tu sistema y qué te obliga a garantizar ese tipo. Un sistema de información y un sistema crítico no se diseñan igual.*

**Tipo de sistema: De información**
**Software a la medida: Se construye para un cliente específico que paga por él y define lo que necesita. El éxito se mide por si resuelve el problema de ese cliente.**

*(De información · Embebido · Crítico · Web y SaaS · De datos y análisis)*

**Por qué es de ese tipo: Su función central es capturar, almacenar y mostrar información (inventario y ventas por categoría) para apoyar la decisión humana de reabastecer o no un producto.**

**Atributos de calidad que impone: Usabilidad y Flexibilidad de datos**

| Atributo | Por qué importa en mi caso | Qué pasa si no se cumple |
|---|---|---|
|Usabilidad |Se usa en mostrador, entre cliente y cliente, con productos de categorías muy distintas que capturar rápido |Si registrar un producto nuevo es lento o confuso, terminarás sin actualizar el inventario y perderá utilidad |
|Flexibilidad de datos |Cada categoría tiene variantes distintas (talla en ropa, modelo en relojes, color en gorras y collares) |Si el sistema solo soporta un tipo de variante, no podrás registrar bien todas las categorías del negocio |

**Reglas de negocio que ya identifiqué:**

*Instrucción: reglas que no son obvias desde fuera y que alguien que conoce el dominio tendría que explicarte. Si no encuentras ninguna, tu caso puede ser demasiado simple.*

1. Un mismo producto (por ejemplo, una playera) puede existir en varias tallas y/o colores, y cada combinación se controla como stock independiente, no como un solo número general.
2. El nivel mínimo de stock para avisar reabastecimiento no es igual para todas las categorías: un reloj de edición limitada puede tener mínimo de 1 unidad, mientras que una gorra básica puede tener mínimo de 5.
3. Una venta no debe poder registrarse si deja el stock de esa variante específica en negativo, para evitar errores de conteo.

---

## 5. Ciclo de vida elegido

*Instrucción: este apartado se trabaja en la semana 3, después de ver los modelos de desarrollo. La justificación pesa más que la elección: no hay un modelo correcto, hay uno defendible para tu caso.*

**Modelo elegido:Prototipado Rapido**

**Por qué le conviene a este proyecto:Soy solo una persona desarrollandolo y el cliente está disponible en todo momento para dar retroalimentación inmediata. Los requisitos base son claros (inventario y ventas), pero al manejar categorías tan distintas entre sí es probable que descubra ajustes necesarios sobre la marcha, y con esto tener una version desechable ayudaria a que de manera mas sencilla se puedan realizar los ajustes necesarios una vez que se use el sistema en la tienda real. Un modelo rapido permite tener primero lo mínimo funcional (registrar producto y venta) y después ir sumando alertas y reportes sin detener el uso diario del sistema.**

*Instrucción: argumenta con las características reales de tu caso. Estabilidad de los requisitos, disponibilidad del cliente, nivel de riesgo, tamaño del equipo, frecuencia de entregas esperada.*

### Alternativas descartadas

**Alternativa 1:cascada**

*Por qué la descarté:Exige tener todos los requisitos definidos y congelados desde el inicio, pero al manejar categorías de producto tan variadas (ropa, relojes, collares, gorras), es muy probable que los requisitos de captura se ajusten una vez que el sistema esté en uso real; con cascada habría que rehacer fases completas cada vez.*

**Alternativa 2:V model**

*Por qué la descarté: Está diseñado para sistemas donde la verificación y validación formal son mas formales y las cuatro actividades ocurren una sola vez, en orden estricto. Cada fase produce un documento que se aprueba antes de pasar a la siguiente generando que tenga ms probabilidad de alguien audita o certifica el sistema. nadie audita ni certifica UnikStock, ese nivel de rigor de pruebas formales no tiene justificación aquí  sería mas desarrollo y temas para una herramienta interna de una sola tienda.*

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
