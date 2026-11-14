## Lo que cuenta como un sustantivo

Un **anatomical part**: un rango nombrado del contorno del glifo, o una línea de referencia nombrada de ancho de fuente con la que se mide el contorno.Existen once en este territorio - nueve vivos, uno sobrante, un fantasma.

Dos tipos de sustantivos:

- **Stroke parts** (tallo, cuenco, terminal, terminal de bola, espolón) — un tramo contiguo del contorno exterior.
- **Derived shapes** (contador, apertura) — espacio en blanco delimitado por partes de trazo, sin contorno propio.
- **Metrics** (x-height, baseline, overshoot) — líneas de referencia horizontales de las propias tablas de la fuente, no el contorno del glifo en absoluto.

## Lo que cuenta como movimiento

La edición de una parte de trazo cambia el rango de contorno que nombra, y cualquier cosa que el rango bordee estructuralmente. Un tallo que comparte un borde con el contador significa que ensanchar el tallo estrecha el contador — eso es un verdadero éxito, citarlo. Un tronco que no comparte nada con la altura x significa que cambiar el tallo nunca lo toca — eso es una verdadera falta, citarlo también.

Las métricas se mueven de manera diferente: afectan *a cada glifo de la fuente*, nunca solo a éste. Esa asimetría —un cambio de trazo de un glifo se mantiene local, un cambio de métrica de toda la fuente se vuelve global— es lo más importante que una carta en este territorio puede hacer bien.

## Live / Remanente / Fantasma, definido para este territorio

- **Live** — La parte corresponde a un rango real del contorno real, citable por índice de puntos y coordenadas.
- **Leftover** — La parte es real y presente, pero su razón de existir es una corrección de una tradición de diseño anterior, no una característica de este glifo por sí mismo.El exceso: todavía haciendo su trabajo, todavía vale la pena explicar, no algo para "arreglar".
- **Ghost** — El fantasma de este territorio, el serif de pie, existe precisamente porque la propia categoría de la tipografía (serif de placa) establece una expectativa que esta letra no cumple, y por lo tanto, el tipo de letra tiene un nombre que un lector alcanzará, y nada detrás de él en este glifo específico.

## Golpes / No golpea

Cada tarjeta termina con exactamente dos líneas: **Hits** nombra al verdadero vecino estructural y **Does not hit** nombra al vecino incorrecto que el lector adivinaría primero, por lo general la parte que parece adyacente en la forma de letra renderizada pero no comparte ningún límite real en los datos del esquema.

## Denegados

- No pegar los datos de ruta sin procesar del glifo en una tarjeta como si fuera una explicación — citar rangos de puntos y límites, la misma disciplina que citar una ruta de archivo en lugar de pegar un script.
- No se trata una forma derivada (contador, abertura) como si tuviera geometría independiente para editar.
- Una parte que no existe recibe una tarjeta que lo dice, no el silencio, y la parte que existe recibe la carta que lo dice.

## Cómo se construye una tarjeta

Antes de escribir cualquier tarjeta: extraer el contorno real (`fontTools`, no una imagen renderizada, no una memoria de cómo Clarendon "debería" verse), identificar qué rango de puntos ocupa la parte, y comprobarlo con una segunda fuente independiente de la misma fuente antes de confiar en cualquier cosa que parezca sorprendente.La tarjeta fantasma de este territorio existe porque esa comprobación era necesaria - la primera mirada al contorno parecía equivocada precisamente donde en realidad estaba correcta.
