## DECISIONES

Registrado por la forma de registro de decisión de `icm-md-writer`, de modo que una sesión posterior no vuelva a argumentar o invierta silenciosamente ninguna de las llamadas.

---

**Decision:** Map Clarendon LT Std (`ClarendonLTStd.otf`, Adobe), not Ringold (`Ringold-Clarendon`, Bijou Type).

**Context:** Adobe Fonts returned two “Clarendon” matches. Ringold is a 2020s Bijou Type design by Dan Rhatigan with a style cut named “Clarendon”; Clarendon URW / Clarendon LT Std are digitizations of the original 1845 Fann Street Foundry design.

**Options considered:** Ringold (available, contemporary reinterpretation), Clarendon URW (Adobe Fonts, faithful digitization), Clarendon LT Std (found locally, same lineage as URW's source).

**Rationale:** El brief era "la serif clásica de la losa" - el original histórico, no un tipo de letra contemporáneo que tomó prestado su nombre para un corte.Clarendon LT Std se confirmó en la propia máquina del usuario y se verificó con una segunda fuente independiente (SuperClarendon) antes de su uso.

**Consequences:** Every card in `objects/` cites `ClarendonLTStd.otf` specifically. A card built from Ringold's outline would not match — the shapes differ (this was tested: Ringold's lowercase a follows the general double-storey pattern but its terminal geometry is not identical).

---

**Decision:** Cambie el nombre de “Arch” → **Finial**, “Tail”→ **Spur**.

**Context:** Ambas cartas fueron redactadas primero a partir de conocimientos tipográficos generales, luego auditadas contra la habilidad cargada `typography-fundamentals` de `glossary.md`, la fuente en la que se supone que está basado todo este mapa.

**Options considered:** Mantener "Arco" y "Colar" (términos comunes, posiblemente más claros para un lector profano) vs. cambiar a los términos definidos por la propia habilidad.

**Rationale:** `glossary.md` does not define “Arch” at all. It defines **Finial** — “an ornamental terminal stroke at the top of characters such as *a* and *f*” — explicitly for this letter. It defines **Tail** only for Q, K, R, and g's loop, not for *a*; it defines **Spur** as “the terminal to the stem of a rounded letter,” which is the correct fit. `rules.md` for this territory says a card must cite grounded terminology, not memory — using “Arch” and “Tail” would have violated this map's own rule.

**Consequences:** `reference/naming-collisions.md` documenta ambos intercambios como la colisión que un lector probablemente golpeará primero, ya que “arco” y “cola” son las palabras que la mayoría de la gente alcanza por analogía a *n*/*m*/*h* y *g*/*Q* respectivamente.

---

**Decision:** Vuelva a derivar las regiones del tallo y de la terminación a partir de un escaneo punto-en-polígono del contorno real, reemplazando los cuadros delimitadores que se colocaron a simple vista.

**Context:** Building the live diagram surfaced that `stem`'s hover region (`x: 428, y: 52, w: 145, h: 306`) mostly covered background, not ink — its anchor and clip rectangle had been eyeballed from the earlier text-only coordinate walk rather than checked against the actual filled shape. A systematic scan (`fontTools` outline, ray-casting point-in-polygon, counter treated as a hole) found the stem's real ink at mid-height spans only x=302–440, not the x=428–573 range the original card used — the card had conflated the glyph's overall right bound (556, which belongs to the spur) with the stem's own edge.

**Options considered:** Parchear la tarjeta en aislamiento vs. volver a escanear el ancla y la región de cada tarjeta de trazo contra el mismo método.

**Rationale:** Si una región colocada a mano estaba mal, las otras se construyeron de la misma manera y justificaron la misma comprobación, no solo la que un usuario notó por casualidad. Las cinco anclas de trazo se volvieron a verificar por punto-en-polígono; cuatro (bowl, finial, terminal de bola, espolón) ya se encontraban en tinta real, pero el rectángulo de la región del finial se apretó para que coincidiera con su proporción de tinta real (~52% vs. el original del vástago ~0%). Un rectángulo no puede enmarcar perfectamente un trazo curvo — el finial y el bowl ambos aterrizan cerca del 50% de cobertura de tinta incluso si se ajustan correctamente, porque sus lados cóncavos necesariamente atraen algo de fondo.

**Consequences:** `objects/stem.md` y `objects/finial.md` fueron reescritos con el frontmatter `anchor`/`region` corregido y la prosa corregida (la afirmación de la antigua carta principal de que su borde derecho alcanzaba x=556 era incorrecta y se llama en la propia tarjeta en lugar de arreglarla silenciosamente).

---

**Decision:** Cap `stem`'s region at y≥165 and `spur`'s at y≤165, instead of letting both run through y=60–165.

**Context:** The corrected stem region above still spanned y=60–355, which overlaps `spur`'s region (y=−22–190) across x=332–440 — the exact band where the spur's curl lifts off the stem's base. Hotspots are layered in DOM order, so within that overlap `spur`'s hotspot (added later) always won, making `stem` unreachable by hover in its lower third even though its region rectangle was, on paper, mostly on-ink.

**Options considered:** Reordena el DOM para que las pinturas de tallo sean las últimas (arregla el síntoma, no la causa — solo invierte qué parte se vuelve inalcanzable); encoge una región arbitrariamente; divide el rango y en el punto real que separa la tinta de los dos trazos.

**Rationale:** El escaneo del segmento (la entrada anterior de `reference/decisions.md`) muestra que la tinta del espolón existe como una isla aislada separada del tallo solo por debajo de y≈165; por encima de eso, solo el propio segmento del tallo continúa.Dividiendo las dos regiones en y=165 se elimina la superposición por completo en lugar de recubrirla con orden z.

**Consequences:** La altura de la región `objects/stem.md` se redujo a 185 (y:165–350); la altura de la zona `objects/spur.md` se redujo al 187 (y:−22–165).

---

**Decision:** Highlight rendering switched from a hard `clip-path` to a blurred `mask` (feGaussianBlur, stdDeviation 16) for every rect/circle region.

**Context:** Once the highlights were actually visible (previous entry), the boundary itself was still wrong in a different way: a region's straight edge frequently has no anatomical meaning — it exists only to stop the highlight from bleeding into a neighbouring part (e.g. the stem/spur split at y=165, which sits mid-curve on a single unbroken vertical stroke with no real joint there). A hard clip made that arbitrary cut look like a rectangle had been pasted over the letter, most visibly on `spur`, whose highlight had a flat horizontal top slicing straight across the curl.

**Options considered:** (1) trazar a mano los verdaderos sub-trazados desde los comandos de bezier reales de la fuente para que cada borde siga la tinta real — investigado directamente contra los datos de trayecto sin procesar; rechazado por ahora porque varias partes (la espiral de la bola-terminal en particular) se doblan sobre sí mismas de una manera que no se reduce a cortes limpios de índice de puntos sin riesgo real de introducir huecos o auto-intersecciones que son difíciles de verificar visualmente. (2) Elipses en lugar de rectas — mejor que rectas en partes curvas, todavía un borde duro arbitrario. (3) Máscara suave en lugar de clip duro.

**Rationale:** Una máscara con un rectángulo/círculo borroso mantiene cada borde de tinta *verdadero* exactamente tan nítido como antes — la máscara está a plena opacidad mucho antes de que llegue a la silueta real — y solo suaviza la opacidad cerca del propio límite artificial, donde no existe ningún borde real que preservar. Esto se lee como “el área general de este trazo” en lugar de “este rectángulo exacto”, lo cual es lo honesto de afirmar dado que el límite realmente es una llamada de juicio, no un hecho medido. La técnica de contrapunteo de la entrada anterior no se ve afectada: tanto el relleno de acento como el punteo de color de fondo comparten la misma máscara, por lo que el propio borde verdadero del contador permanece nítido en todo momento — confirmado por zoom visual directo, no solo inspección DOM.

**Consequences:** `defs` now emits one shared `<filter id="soft-edge">` plus one `<mask>` per stroke card (replacing the old `<clipPath>` per card); `fillPath`/`punch` use `mask="url(#mask-ID)"` instead of `clip-path`. No card content changed — this is purely a rendering technique, not a re-scoping of any region.

---

**Decision:** Reemplace la máscara borrosa (entrada anterior) con un clip `ellipse` con bordes duros para `bowl`, `finial` y `spur`; `stem` sigue siendo un `rect` literal.

**Context:** El desenfoque solucionó el problema del "rectángulo obvio", pero introdujo uno nuevo: un brillo suave y borroso se lee como impreciso, y choca con el resto del lenguaje nítido y plano del diagrama (relleno sólido Clarendon, etiquetas sólidas Akzidenz, recorte de contador con bordes duros).

**Options considered:** Un radio de desenfoque más pequeño (aún suave, solo menos); subtrazados verdaderos trazados a mano desde los comandos bezier reales de la fuente (investigados y rechazados en la entrada anterior — la espiral del terminal de la bola no se reduce a cortes limpios); una forma con bordes duros más adecuada para un trazo curvo que un rectángulo alineado con el eje.

**Rationale:** A rectangle has flat sides, so any edge that crosses a stroke does so as a dead-straight cut — the artifact that made `spur` look like a box. An ellipse has no flat sides: wherever its boundary crosses the stroke, it does so at an angle, which reads as a rounded, deliberate highlight rather than a pasted-on shape, while staying exactly as hard-edged and “measured” as the rest of the diagram. `stem` is excluded because it's genuinely a straight vertical stroke — a rect is the anatomically correct shape there, not a compromise.

**Consequences:** `objects/bowl.md`, `objects/finial.md`, `objects/spur.md` frontmatter changed `region.shape` from `rect` to `ellipse` (same `x`/`y`/`w`/`h` — now read as an ellipse's bounding box, `cx`/`cy` at its center, `rx`/`ry` at half its width/height). `docs/index.html` gained a shared `regionShapeEl(r)` helper so the clip-path defs, the highlight fill/punch, and the hotspot all build the identical rect/circle/ellipse from one place instead of three separately-maintained branches — the kind of duplication that let the coordinate-space bug (two entries up) go unnoticed as long as it did. The blur filter and per-card masks were removed entirely.

---

**Decision:** Tire del borde izquierdo de `stem` desde x=320 a x=328, estrechando su región de 120 a 112 de ancho.

**Context:** `stem`'s region and `counter`'s bounds (x=157–323) overlapped by 3 units (320–323). The counter-punch (two entries up) already prevents solid fill from painting over the counter's true hole even there, so this was never a color-accuracy bug — but a 3-unit sliver where a rounded-rect corner nearly grazes a curved hole is exactly the kind of imprecision that reads as visually unsettled up close, and it was flagged as such.

**Rationale:** `stem` y `counter` realmente comparten un borde en la anatomía — la propia línea de Hits de `objects/stem.md` lo dice (“el borde izquierdo del tallo es también la pared derecha del contador”). La solución no es negar esa adyacencia, solo dejar de representarla como un casi-fallo. Volviendo a ejecutar la comprobación de la relación de tinta en los límites extraídos (x=328, w=112) encontré una cobertura de tinta del 100%, más ajustada que el 92% de la región original de 120 de ancho — las 3 unidades que se recortaron nunca fueron tinta de tallo sólido a esta altura de todos modos.

**Consequences:** El ancho de la región `objects/stem.md` cambió de 120→112, x 320→328. Anchor (380,210) re-confirmó en tinta. No se necesitaron cambios de prosa — el rango de tinta citado de la tarjeta (x=324–440 a y=210) ya era preciso; solo la región de renderizado, un subconjunto deliberadamente conservador de la misma, se movió.
