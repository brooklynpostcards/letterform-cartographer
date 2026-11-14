## Decisões

Registrado pela forma de registro de decisão do `icm-md-writer` - para que uma sessão posterior não re-argumente ou silenciosamente reverta qualquer chamada.

---

**Decision:** Map Clarendon LT Std (`ClarendonLTStd.otf`, Adobe), not Ringold (`Ringold-Clarendon`, Bijou Type).

**Context:** Adobe Fonts returned two “Clarendon” matches. Ringold is a 2020s Bijou Type design by Dan Rhatigan with a style cut named “Clarendon”; Clarendon URW / Clarendon LT Std are digitizations of the original 1845 Fann Street Foundry design.

**Options considered:** Ringold (available, contemporary reinterpretation), Clarendon URW (Adobe Fonts, faithful digitization), Clarendon LT Std (found locally, same lineage as URW's source).

**Rationale:** O briefing foi "o clássico slab serif" - o original histórico, não uma fonte contemporânea que tomou seu nome emprestado para um corte.Clarendon LT Std foi confirmado na própria máquina do usuário e verificado contra uma segunda fonte independente (SuperClarendon) antes do uso.

**Consequences:** Every card in `objects/` cites `ClarendonLTStd.otf` specifically. A card built from Ringold's outline would not match — the shapes differ (this was tested: Ringold's lowercase a follows the general double-storey pattern but its terminal geometry is not identical).

---

**Decision:** Rename “Arch” → **Finial**, “Tail” → **Spur**.

**Context:** Ambos os cards foram criados primeiro a partir do conhecimento tipográfico geral, depois auditados contra o `glossary.md` da habilidade `typography-fundamentals` carregada — a fonte em que todo este mapa deve ser baseado.

**Options considered:** Mantenha "Arch" e "Tail" (termos comuns, possivelmente mais claros para um leitor leigo) vs. mude para os próprios termos definidos da habilidade.

**Rationale:** `glossary.md` does not define “Arch” at all. It defines **Finial** — “an ornamental terminal stroke at the top of characters such as *a* and *f*” — explicitly for this letter. It defines **Tail** only for Q, K, R, and g's loop, not for *a*; it defines **Spur** as “the terminal to the stem of a rounded letter,” which is the correct fit. `rules.md` for this territory says a card must cite grounded terminology, not memory — using “Arch” and “Tail” would have violated this map's own rule.

**Consequences:** O `reference/naming-collisions.md` documenta ambos os swaps como a colisão que um leitor provavelmente atingirá primeiro, já que “arch” e “tail” são as palavras que a maioria das pessoas alcança por analogia com *n*/*m*/*h* e *g*/*Q*, respectivamente.

---

**Decision:** Re-derive as regiões de haste e terminais a partir de uma varredura ponto-em-polígono do contorno real, substituindo as caixas delimitadoras que foram colocadas a olho nu.

**Context:** Building the live diagram surfaced that `stem`'s hover region (`x: 428, y: 52, w: 145, h: 306`) mostly covered background, not ink — its anchor and clip rectangle had been eyeballed from the earlier text-only coordinate walk rather than checked against the actual filled shape. A systematic scan (`fontTools` outline, ray-casting point-in-polygon, counter treated as a hole) found the stem's real ink at mid-height spans only x=302–440, not the x=428–573 range the original card used — the card had conflated the glyph's overall right bound (556, which belongs to the spur) with the stem's own edge.

**Options considered:** Repare o cartão isoladamente vs. re-scan a âncora e região de cada cartão de traço contra o mesmo método.

**Rationale:** Se uma região colocada à mão estivesse errada, as outras eram construídas da mesma forma e exigiam a mesma verificação, não apenas aquela que um usuário percebeu. Todas as cinco âncoras de traço foram re-verificadas por ponto-em-polígono; quatro (bowl, finial, terminal de esfera, spur) já estavam em tinta real, mas o retângulo da região do finial foi apertado para combinar com sua proporção de tinta real (~52% vs. ~0% original do stem). Um retângulo não pode encaixar perfeitamente um traço curvo — o finial e o bowl ambos aterram perto de 50% de cobertura de tinta, mesmo corretamente ajustados, porque seus lados côncavos necessariamente puxam algum fundo. Isso é esperado para um clipe reto em uma letra curva, não um defeito.

**Consequences:** `objects/stem.md` e `objects/finial.md` foram reescritas com o frontmatter `anchor`/`region` corrigido e a prosa corrigida (a alegação do antigo card de raiz de que sua borda direita atingiu x=556 estava errada e é chamada no próprio card em vez de ser silenciosamente corrigida).

---

**Decision:** Cap `stem`'s region at y≥165 and `spur`'s at y≤165, instead of letting both run through y=60–165.

**Context:** The corrected stem region above still spanned y=60–355, which overlaps `spur`'s region (y=−22–190) across x=332–440 — the exact band where the spur's curl lifts off the stem's base. Hotspots are layered in DOM order, so within that overlap `spur`'s hotspot (added later) always won, making `stem` unreachable by hover in its lower third even though its region rectangle was, on paper, mostly on-ink.

**Options considered:** Reordene o DOM para que as pinturas de haste fiquem por último (corrige o sintoma, não a causa — apenas inverte qual parte se torna inalcançável); encolha uma região arbitrariamente; divida o intervalo y no ponto real em que a tinta dos dois traços se separa.

**Rationale:** A varredura do segmento (entrada anterior de `reference/decisions.md`) mostra que a tinta do esporão existe como uma ilha isolada separada da haste apenas abaixo de y≈165; acima disso, apenas o próprio segmento da haste continua.Dividindo as duas regiões em y=165 remove a sobreposição inteiramente ao invés de cobri-la com ordem z.

**Consequences:** A altura da região `objects/stem.md` encolheu para 185 (y:165–350); a altura da regiões `objects/spur.md` encolheu a 187 (y:−22–165).

---

**Decision:** A renderização de destaque foi trocada de um `clip-path` rígido para uma `mask` desfocada (feGaussianBlur, stdDeviation 16) para cada região rect/circle.

**Context:** Once the highlights were actually visible (previous entry), the boundary itself was still wrong in a different way: a region's straight edge frequently has no anatomical meaning — it exists only to stop the highlight from bleeding into a neighbouring part (e.g. the stem/spur split at y=165, which sits mid-curve on a single unbroken vertical stroke with no real joint there). A hard clip made that arbitrary cut look like a rectangle had been pasted over the letter, most visibly on `spur`, whose highlight had a flat horizontal top slicing straight across the curl.

**Options considered:** (1) traçar manualmente sub-caminhos verdadeiros a partir dos comandos bezier reais da fonte para que cada limite siga a tinta real — investigado diretamente contra os dados brutos do caminho; rejeitado por enquanto porque várias partes (a espiral do terminal esférico em particular) se dobram sobre si mesmas de uma maneira que não reduz a cortes limpos de índice de ponto sem risco real de introduzir lacunas ou auto-intersecções que são difíceis de verificar visualmente. (2) elipses em vez de retas — melhor do que retas em partes curvas, ainda uma borda dura arbitrária. (3) máscara suave em vez de clipe duro.

**Rationale:** Uma máscara com um rectângulo/círculo desfocado mantém cada borda de tinta *verdadeira* exatamente tão nítida quanto antes — a máscara está em total opacidade bem antes de atingir a silhueta real — e apenas diminui a opacidade perto do próprio limite artificial, onde não existe nenhuma borda real para preservar. Isso se lê como “a área geral deste traçado” ao invés de “este retângulo exato”, o que é a coisa honesta a ser afirmada, dado que o limite realmente é uma chamada de julgamento, não um fato medido. A técnica de contraponto da entrada anterior não é afetada: tanto o preenchimento de acento quanto o punch colorido de fundo compartilham a mesma máscara, então a própria borda verdadeira do contador permanece nítida por toda parte — confirmada pelo zoom visual direto, não apenas pela inspeção do DOM.

**Consequences:** `defs` now emits one shared `<filter id="soft-edge">` plus one `<mask>` per stroke card (replacing the old `<clipPath>` per card); `fillPath`/`punch` use `mask="url(#mask-ID)"` instead of `clip-path`. No card content changed — this is purely a rendering technique, not a re-scoping of any region.

---

**Decision:** Substitua a máscara desfocada (entrada anterior) por um clipe `ellipse` com bordas rígidas para `bowl`, `finial` e `spur`; `stem` permanece um `rect` literal.

**Context:** O desfoque corrigiu o problema do “retângulo óbvio”, mas introduziu um novo — um brilho suave e nebuloso é lido como impreciso, e entra em conflito com o resto da linguagem nítida e de cores planas do diagrama (preenchimento Clarendon sólido, rótulos Akzidenz sólidos, recorte de contador com bordas duras).

**Options considered:** Raio de desfoque menor (ainda suave, apenas menos dele); sub-caminhos verdadeiros rastreados à mão a partir dos comandos bezier reais da fonte (investigados e rejeitados na entrada acima — a espiral do terminal da bola não se reduz a cortes limpos); uma forma de bordas duras mais adequada para um traço curvo do que um retângulo alinhado ao eixo.

**Rationale:** A rectangle has flat sides, so any edge that crosses a stroke does so as a dead-straight cut — the artifact that made `spur` look like a box. An ellipse has no flat sides: wherever its boundary crosses the stroke, it does so at an angle, which reads as a rounded, deliberate highlight rather than a pasted-on shape, while staying exactly as hard-edged and “measured” as the rest of the diagram. `stem` is excluded because it's genuinely a straight vertical stroke — a rect is the anatomically correct shape there, not a compromise.

**Consequences:** `objects/bowl.md`, `objects/finial.md`, `objects/spur.md` frontmatter changed `region.shape` from `rect` to `ellipse` (same `x`/`y`/`w`/`h` — now read as an ellipse's bounding box, `cx`/`cy` at its center, `rx`/`ry` at half its width/height). `docs/index.html` gained a shared `regionShapeEl(r)` helper so the clip-path defs, the highlight fill/punch, and the hotspot all build the identical rect/circle/ellipse from one place instead of three separately-maintained branches — the kind of duplication that let the coordinate-space bug (two entries up) go unnoticed as long as it did. The blur filter and per-card masks were removed entirely.

---

**Decision:** Puxe a borda esquerda do `stem` de x=320 para x=328, estreitando sua região de 120 para 112 de largura.

**Context:** `stem`'s region and `counter`'s bounds (x=157–323) overlapped by 3 units (320–323). The counter-punch (two entries up) already prevents solid fill from painting over the counter's true hole even there, so this was never a color-accuracy bug — but a 3-unit sliver where a rounded-rect corner nearly grazes a curved hole is exactly the kind of imprecision that reads as visually unsettled up close, and it was flagged as such.

**Rationale:** `stem` e `counter` realmente compartilham uma borda na anatomia — a própria linha de Hits de `objects/stem.md` diz isso (“a borda esquerda da haste também é a parede direita do balcão”). A correção não é negar essa adjacência, apenas parar de renderizá-la como um quase-erro. Re-executando a verificação da proporção de tinta nos limites puxados (x=328, w=112) encontrou 100% de cobertura de tinta, mais apertada do que os 92% da região original de 120 de largura — as 3 unidades sendo cortadas nunca foram tinta de haste sólida nessa altura de qualquer maneira.

**Consequences:** A largura da região `objects/stem.md` foi alterada de 120 para 112, x 320→328. Âncora (380,210) re-confirmada na tinta. Nenhuma mudança de prosa era necessária — a faixa de tinta citada do cartão (x=324–440 a y=210) já era precisa; apenas a região de renderização, um subconjunto deliberadamente conservador dela, foi movida.
