# Letterform Cartographer

Un mapa de sistema de un glifo: la letra minúscula **a** en Clarendon LT Std romano.Once cartas de sustantivos —nueve vivas, una sobrante, una fantasma— cada una citando un rango exacto del contorno de la fuente real, no una aproximación redibujada de la misma.

## Demostración en vivo

`docs/index.html` — un diagrama flotante de la carta. Cada hover obtiene y renderiza la tarjeta `.md` real desde `objects/`, en vivo, directamente desde este repositorio. Nada en el diagrama es una copia de las tarjetas; es un visor sobre ellas. Servirlo desde la raíz del repositorio (GitHub Pages: fuente = `/ (root)`, no `/docs`) por lo que la obtención relativa a `../objects/*.md` se resuelve — Las páginas restringidas solo a ZQx5 tendrían un 404 en cada tarjeta.

## Por qué esto existe

“Bowl”, “counter”, “spur” son nombres que un ser humano dibuja alrededor de rangos de esos datos — nada en un archivo de fuentes se etiqueta a sí mismo. Este repositorio es ese etiquetado, hecho una vez, citado contra el contorno extraído real (`fontTools`) y una habilidad de referencia tipográfica cargada, por lo que nadie tiene que volver a derivarlo a simple vista.

## El único fantasma, explicado por adelantado

Clarendon is a slab serif — that's the first and often only thing anyone knows about it, and it creates a confident, wrong expectation: that every stroke in the face ends in a bracketed slab foot. This lowercase `a` doesn't. Its stem ends in a curved spur, its finial ends in a ball terminal, and no foot serif exists anywhere on the letter. That's not a simplification or an artistic choice being described loosely — it's a fact about the actual outline, verified against a second independent Clarendon after the first extraction was nearly discarded as corrupt for lacking the very serif this README just told you not to expect. See [`objects/foot-serif.md`](objects/foot-serif.md) for the full account.

## Cómo un desconocido, o una sesión fría de IA, usa esto

1. Lee `identity.md` y `rules.md` una vez, son cortos.
2. Abre `examples.md`, es una tabla de catálogo de las once piezas más tres paseos cortos trabajados.
3. ¿Necesita una parte? Abra exactamente su tarjeta en `objects/`. Pare allí.
4. Si encuentras un nombre que no está en el catálogo ("arco", "cola"), comprueba primero `reference/naming-collisions.md`, es muy probable que ya esté respondido.

**The one rule: load the catalog, then one card. Never all eleven at once.**

## ¿Qué hay aquí?

| Path | Trabajo |
| --- | --- |
| `identity.md` | Quién es el cartógrafo, cuál es el territorio, quién es el lector posterior |
| `rules.md` | Lo que cuenta como un sustantivo aquí, cómo se deciden Live/Leftover/Ghost, la regla Hits/Does-not-hit |
| `examples.md` | La tabla del catálogo + tres paseos trabajados, fechado 2026-08-21 |
| `objects/` | Las once cartas en sí — los estantes reales |
| `reference/card-types.md` | Las tres formas de cartas que utiliza este territorio |
| `reference/naming-collisions.md` | Cuatro trampas de vocabulario reales, escritas una vez |
| `reference/decisions.md` | Decisiones registradas (elección de fuente; correcciones terminológicas; técnica de renderizado) con justificación |
| `docs/index.html` | El diagrama en vivo — un visor sobre `objects/`, no una copia de él |

## Lo que esto no es

Not a font-design tutorial, not an audit of Clarendon, not a copy of the glyph's data in nicer prose. If a card and the real outline in `ClarendonLTStd.otf` ever disagree, the outline is right and the card is wrong — every numeric claim in `objects/` cites a contour point range or a font table value specifically so that check is possible.

## Territorio y abastecimiento

- Fuente: Clarendon LT Std Roman (`ClarendonLTStd.otf`, Adobe), verificada con un segundo Clarendon independiente antes de su uso — ver `reference/decisions.md`.
- Terminología: habilidad `typography-fundamentals` (glosario, notas de contraforma, referencia de clasificación) Dos términos redactados de memoria antes de esa auditoría (“arco”, “cola”) eran incorrectos y fueron reemplazados por los términos reales de la habilidad (“finial”, “espuela”).
- El diagrama describe el glifo y las once palabras de la etiqueta como trayectorias vectoriales en lugar de incrustar Clarendon o Akzidenz-Grotesk como fuentes web. Ambos son software de fuentes comerciales; solo se envían las formas de letra específicas utilizadas como ilustraciones del diagrama, no las fuentes en sí. El texto del cuerpo de la tarjeta (que es prosa sin límites, no una lista fija de palabras) utiliza una pila de fuentes CSS del sistema: Helvetica Neue, que recae en Helvetica, Arial y sans-serif.

Construido siguiendo la sexta forma descrita en Weekly Comp #11: The Cartographer — un mapa de sistema de un cuerpo de trabajo real y en vigor, usando los invariantes de la habilidad ICM Architect (github.com/RinDig/icm-architect) como andamio.
