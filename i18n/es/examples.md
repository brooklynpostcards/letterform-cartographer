## Mapa trabajado — Clarendon minúscula `a`

Territorio: un glifo, `ClarendonLTStd.otf`, citado el 21-08-2026. Once cartas viven en [`objects/`](objects/) — este archivo es el catálogo, no una copia de ellas. Terminología auditada contra el glosario de habilidades de `typography-fundamentals`; dos términos redactados de memoria (“arco”, “cola”) eran incorrectos y fueron reemplazados — ver [`reference/decisions.md`](reference/decisions.md).

### Catálogo

| Parte 1 | Tipo | Status | Tarjeta |
| ------------- | --------------- | ----------------- | -------------------------------------------------------- |
| Voto | accidente cerebrovascular | 2012-2013: en vivo | [`objects/stem.md`](objects/stem.md)                      |
| Bowl | accidente cerebrovascular | 2012-2013: en vivo | [`objects/bowl.md`](objects/bowl.md)                      |
| Finial | accidente cerebrovascular | 2012-2013: en vivo | [`objects/finial.md`](objects/finial.md)                  |
| Terminal de bola | Terminación del trazo | 2012-2013: en vivo | [`objects/ball-terminal.md`](objects/ball-terminal.md)    |
| Track | Terminación del trazo | 2012-2013: en vivo | [`objects/spur.md`](objects/spur.md)                      |
| Contador | Espacio negativo |  en vivo, derivado | [`objects/counter.md`](objects/counter.md)                |
| Apertura | Espacio negativo |  en vivo, derivado | [`objects/aperture.md`](objects/aperture.md)              |
| x-altura | métrica | Live | [`objects/x-height.md`](objects/x-height.md)              |
| Base de referencia | métrica | 2012-2013: en vivo | [`objects/baseline.md`](objects/baseline.md)              |
| Overshoot | corrección | Resto | [`objects/overshoot.md`](objects/overshoot.md)            |
| Foot serif | accidente cerebrovascular | 👻 fantasma | [`objects/foot-serif.md`](objects/foot-serif.md)          |

Un lector frío se detiene aquí a menos que una parte necesite abrirse.

### Una caminata, en su totalidad

*Pregunta: "Quiero darle a este Clarendon `a` un pie de losa más pesado para que coincida con el resto de la cara, ¿qué toca eso?"*

1. Abre el catálogo de arriba. “Foot serif” es la puerta obvia.
2. Abre `objects/foot-serif.md`. Dice, en la primera línea del cuerpo del texto: no hay serifa de pie en este glifo. Estado: **ghost**.
3. La tarjeta también nombra los dos trazos reales que un lector podría haber querido decir en su lugar: [`spur`](objects/spur.md) y [`ball-terminal`](objects/ball-terminal.md), y explica, con una cita de un paseo por las coordenadas, por qué ninguno de ellos es un serif.

No se tuvo que abrir ninguna otra tarjeta para responder a esto, ese es el punto del catálogo.

### Una segunda caminata, más corta

**Question:** "¿Cuál es el contador, y puedo hacerlo más grande por su cuenta?"

1. Abre `objects/counter.md`.
2. **Hits**: Nada directamente — se deriva de `bowl` y `stem`.
3. **Does not hit**: La apertura, una forma blanca separada que la gente suele significar en su lugar.
4. Respuesta: no, no por sí solo. Edite `bowl` o `stem`; el contador sigue.

### Una tercera caminata, sobre el vocabulario en sí

**Question:** "¿Cómo se llama el arco en este a?"

1. No hay `arch.md`. El catálogo no tiene una fila llamada "Arch".
2. `reference/naming-collisions.md` nombra esta pregunta exacta y apunta a [`objects/finial.md`](objects/finial.md), el término basado en habilidades para esta carta, con la razón de que "arco" no se aplica aquí (nunca vuelve a la línea base, por lo que no es uno).
3. Parar, con el vocabulario corregido, no solo la geometría localizada.
