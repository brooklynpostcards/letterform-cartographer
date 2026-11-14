## Entscheidungen

Protokolliert per `icm-md-writer`'s Decision Record Shape - so dass eine spätere Sitzung keinen der Aufrufe erneut argumentiert oder stillschweigend rückgängig macht.

---

**Decision:** Map Clarendon LT Std (`ClarendonLTStd.otf`, Adobe), not Ringold (`Ringold-Clarendon`, Bijou Type).

**Context:** Adobe Fonts returned two “Clarendon” matches. Ringold is a 2020s Bijou Type design by Dan Rhatigan with a style cut named “Clarendon”; Clarendon URW / Clarendon LT Std are digitizations of the original 1845 Fann Street Foundry design.

**Options considered:** Ringold (available, contemporary reinterpretation), Clarendon URW (Adobe Fonts, faithful digitization), Clarendon LT Std (found locally, same lineage as URW's source).

**Rationale:** Das Briefing lautete „the classic slab serif“ – das historische Original, nicht eine zeitgenössische Schrift, die ihren Namen für einen Schnitt geliehen hat.Clarendon LT Std wurde auf dem eigenen Rechner des Benutzers bestätigt und vor der Verwendung mit einer zweiten unabhängigen Quelle (SuperClarendon) überprüft.

**Consequences:** Jede Karte in `objects/` zitiert `ClarendonLTStd.otf` ausdrücklich. Eine Karte, die aus dem Umriss von Ringold gebaut wurde, würde nicht passen - die Formen unterscheiden sich (dies wurde getestet: Das Kleinbuchstabe a von ZQx2 folgt dem allgemeinen zweistöckigen Muster, aber seine Terminalgeometrie ist nicht identisch).

---

**Decision:** Umbenennen Sie “Bogen” → **Finial**, “Schwanz” →**Spur**.

**Context:** Beide Karten wurden zuerst aus allgemeinem typografischen Wissen entworfen und dann mit dem geladenen `typography-fundamentals` Skill `glossary.md` verglichen - der Quelle, auf der diese ganze Karte basieren soll.

**Options considered:** Behalten Sie "Bogen" und "Schwanz" (allgemeine Begriffe, die für einen Laien wahrscheinlich klarer sind) und wechseln Sie zu den eigenen definierten Begriffen der Fertigkeit.

**Rationale:** `glossary.md` does not define “Arch” at all. It defines **Finial** — “an ornamental terminal stroke at the top of characters such as *a* and *f*” — explicitly for this letter. It defines **Tail** only for Q, K, R, and g's loop, not for *a*; it defines **Spur** as “the terminal to the stem of a rounded letter,” which is the correct fit. `rules.md` for this territory says a card must cite grounded terminology, not memory — using “Arch” and “Tail” would have violated this map's own rule.

**Consequences:** `reference/naming-collisions.md` dokumentiert beide Swaps als die Kollision, auf die ein Leser wahrscheinlich zuerst trifft, da “arch” und “tail” die Wörter sind, nach denen die meisten Menschen analog zu *n*/*m*/*h* und *g*/*Q* greifen.

---

**Decision:** Legen Sie die Stamm- und Endregionen aus einem Point-in-Polygon-Scan der echten Kontur neu ab und ersetzen Sie dabei Begrenzungsrahmen, die mit dem Auge platziert wurden.

**Context:** Building the live diagram surfaced that `stem`'s hover region (`x: 428, y: 52, w: 145, h: 306`) mostly covered background, not ink — its anchor and clip rectangle had been eyeballed from the earlier text-only coordinate walk rather than checked against the actual filled shape. A systematic scan (`fontTools` outline, ray-casting point-in-polygon, counter treated as a hole) found the stem's real ink at mid-height spans only x=302–440, not the x=428–573 range the original card used — the card had conflated the glyph's overall right bound (556, which belongs to the spur) with the stem's own edge.

**Options considered:** Patchen Sie die eine Karte isoliert oder scannen Sie den Anker und die Region jeder Strichkarte mit derselben Methode erneut.

**Rationale:** Wenn ein von Hand platzierter Bereich falsch war, wurden die anderen auf die gleiche Weise gebaut und erforderten die gleiche Prüfung, nicht nur derjenige, den ein Benutzer zufällig bemerkte. Alle fünf Strich-Anker wurden durch Point-in-Polygon erneut überprüft; vier (Schüssel, Endstück, Kugelanschluss, Sporn) saßen bereits auf echter Tinte, aber das Rechteck des Endstücks wurde so angezogen, dass es seinem tatsächlichen Tintenverhältnis entsprach (~52% gegenüber dem Original ~0% des Stiels). Ein Rechteck kann einen gekrümmten Strich nicht perfekt umschließen - Endstück und Schale landen beide bei einer Tintendeckung von etwa 50%, selbst wenn sie korrekt angepasst sind, da ihre konkaven Seiten notwendigerweise etwas Hintergrund einziehen.

**Consequences:** `objects/stem.md` und `objects/finial.md` wurden mit korrigiertem `anchor`/`region` Frontmatter und korrigierter Prosa neu geschrieben (die Behauptung der alten Stammkarte, dass ihre rechte Kante x=556 erreichte, war falsch und wird in der Karte selbst aufgerufen, anstatt stillschweigend behoben zu werden).

---

**Decision:** `stem`'s Region bei y≥165 und `spur`'s bei y≤165 eingrenzen, anstatt beide durch y=60–165. laufen zu lassen

**Context:** The corrected stem region above still spanned y=60–355, which overlaps `spur`'s region (y=−22–190) across x=332–440 — the exact band where the spur's curl lifts off the stem's base. Hotspots are layered in DOM order, so within that overlap `spur`'s hotspot (added later) always won, making `stem` unreachable by hover in its lower third even though its region rectangle was, on paper, mostly on-ink.

**Options considered:** Ordnen Sie das DOM so um, dass die Stammfarben zuletzt angewendet werden (fixiert das Symptom, nicht die Ursache – nur der Teil, der unerreichbar wird, wird umgedreht); verkleinern Sie eine Region beliebig; teilen Sie den y-Bereich an dem Punkt, an dem sich die Tinte der beiden Striche trennt.

**Rationale:** Der Segment-Scan (`reference/decisions.md`'s früherer Eintrag) zeigt, dass die Tinte des Sporns nur unterhalb von y≈165 als isolierte Insel vom Stamm getrennt existiert. Darüber hinaus setzt sich nur das eigene Segment des Stammes fort. Die Trennung der beiden Regionen bei y=165 entfernt die Überlappung vollständig, anstatt sie mit z-Ordung zu überlagern.

**Consequences:** Die Höhe der Region `objects/stem.md` wurde auf 185 (y:165–350) reduziert; die Höhe der Zone `objects/spur.md` wurde auf 22–165 reduziert.Beide Anker wurden nach der Änderung erneut überprüft.

---

**Decision:** Das Highlight-Rendering wurde von einem harten `clip-path` auf ein unscharfes `mask` (feGaussianBlur, stdDeviation 16) für jeden Rechteck-/Kreisbereich umgeschaltet.

**Context:** Once the highlights were actually visible (previous entry), the boundary itself was still wrong in a different way: a region's straight edge frequently has no anatomical meaning — it exists only to stop the highlight from bleeding into a neighbouring part (e.g. the stem/spur split at y=165, which sits mid-curve on a single unbroken vertical stroke with no real joint there). A hard clip made that arbitrary cut look like a rectangle had been pasted over the letter, most visibly on `spur`, whose highlight had a flat horizontal top slicing straight across the curl.

**Options considered:** (1) Echte Unterpfade aus den tatsächlichen Bezier-Befehlen der Schrift von Hand nachzeichnen, so dass jede Grenze der echten Tinte folgt — direkt gegen die Rohpfaddaten untersucht; vorerst abgelehnt, weil mehrere Teile (insbesondere die Kugel-Terminal-Spirale) sich auf eine Weise auf sich selbst verdoppeln, die nicht zu sauberen Punkt-Index-Schnitten ohne echtes Risiko der Einführung von Lücken oder Selbstkreuzungen führt, die schwer visuell zu überprüfen sind. (2) Ellipsen anstelle von Geraden — besser als Geraden auf gekrümmten Teilen, immer noch eine willkürliche harte Kante. (3) Weiche Maske anstelle von hartem Clip.

**Rationale:** Eine Maske mit einem unscharfen Rechteck/Kreis hält jede *wahre* Tintenkante genauso scharf wie zuvor – die Maske ist bei voller Deckkraft, lange bevor sie die reale Silhouette erreicht – und verringert die Deckkraft nur in der Nähe der künstlichen Grenze selbst, wo keine echte Kante zu erhalten ist. Dies liest sich als „die allgemeine Fläche dieses Strichs“ anstatt „dieses exakte Rechteck“, was ehrlicherweise zu behaupten ist, da die Grenze wirklich ein Urteilsaufruf ist, nicht eine gemessene Tatsache. Die Gegenstempeltechnik aus dem vorherigen Eintrag ist unberührt: sowohl die Akzentfüllung als auch der hintergrundfarbene Stempel teilen die gleiche Maske, sodass die eigene wahre Kante des Gegenstempels durchgehend scharf bleibt – bestätigt durch direkten visuellen Zoom, nicht nur durch DOM-Inspektion.

**Consequences:** `defs` gibt jetzt einen gemeinsamen `<filter id="soft-edge">` plus einen `<mask>` pro Strichkarte aus (ersetzt den alten `<clipPath>` pro Karte); `fillPath`/`punch` verwenden `mask="url(#mask-ID)"` anstelle von `clip-path`. Kein Karteninhalt geändert — dies ist rein eine Rendertechnik, keine Neu-Scoping einer Region.

---

**Decision:** Ersetzen Sie die unscharfe Maske (vorheriger Eintrag) durch einen `ellipse`-Clip mit harten Kanten für `bowl`, `finial` und `spur`; `stem` bleibt ein wörtliches `rect`.

**Context:** Die Unschärfe behebt das Problem des „offensichtlichen Rechtecks“, führt aber auch ein neues ein – ein weiches, unscharfes Leuchten wird als ungenau gelesen und kollidiert mit dem Rest der klaren, flachen Farbsprache des Diagramms (einfarbige Clarendon-Füllung, einfarbige Akzidenz-Beschriftungen, harte Kanten am Ausschnitt).

**Options considered:** Kleinerer Unschärferadius (immer noch weich, nur weniger davon); handgezeichnete wahre Unterpfade aus den echten Bezier-Befehlen der Schrift (im obigen Eintrag untersucht und abgelehnt — die Kugel-Terminal-Spirale reduziert sich nicht auf saubere Schnitte); eine Form mit harten Kanten, die besser für einen gekrümmten Strich geeignet ist als ein Achsen-ausgerichtetes Rechteck.

**Rationale:** Ein Rechteck hat flache Seiten, so dass jede Kante, die einen Strich kreuzt, dies als einen geraden Schnitt tut – das Artefakt, das `spur` wie einen Kasten aussehen lässt. Eine Ellipse hat keine flachen Seiten: wo immer ihre Grenze den Strich kreizt, tut sie dies in einem Winkel, der sich als abgerundeter, bewusster Akzent anstatt einer eingeklebten Form liest, während er genauso kantenstark und „gemessen“ bleibt wie der Rest des Diagramms. `stem` wird ausgeschlossen, weil es wirklich ein gerader vertikaler Strich ist – eine gerade Linie ist hier die anatomisch korrekte Form, kein Kompromiss.

**Consequences:** `objects/bowl.md`, `objects/finial.md`, `objects/spur.md` frontmatter changed `region.shape` from `rect` to `ellipse` (same `x`/`y`/`w`/`h` — now read as an ellipse's bounding box, `cx`/`cy` at its center, `rx`/`ry` at half its width/height). `docs/index.html` gained a shared `regionShapeEl(r)` helper so the clip-path defs, the highlight fill/punch, and the hotspot all build the identical rect/circle/ellipse from one place instead of three separately-maintained branches — the kind of duplication that let the coordinate-space bug (two entries up) go unnoticed as long as it did. The blur filter and per-card masks were removed entirely.

---

**Decision:** Pull `stem`'s left edge in from x=320 to x=328, narrowing its region from 120 to 112 wide.

**Context:** `stem`'s region and `counter`'s bounds (x=157–323) overlapped by 3 units (320–323). The counter-punch (two entries up) already prevents solid fill from painting over the counter's true hole even there, so this was never a color-accuracy bug — but a 3-unit sliver where a rounded-rect corner nearly grazes a curved hole is exactly the kind of imprecision that reads as visually unsettled up close, and it was flagged as such.

**Rationale:** `stem` und `counter` teilen sich in der Anatomie eine Grenze – `objects/stem.md`s eigene Hits-Zeile sagt das („der linke Rand des Schafts ist auch die rechte Wand des Zählers“). Die Korrektur besteht nicht darin, diese Nachbarschaft zu leugnen, sondern nur, sie nicht mehr als Beinahe-Versehen zu rendern. Bei einer erneuten Durchführung der Farbverhältnisprüfung an den eingezogenen Grenzen (x=328, w=112) wurde eine 100%ige Farbabdeckung gefunden, die enger als die ursprünglichen 92% des 120-breiten Bereichs war – die 3 getrimmten Einheiten waren sowieso niemals feste Stammfarbe auf dieser Höhe.

**Consequences:** `objects/stem.md`-Bereichsbreite geändert von 120 auf 112, x 320 → 328. Anker (380,210) bestätigt On-Ink. Keine Prosa-Änderungen erforderlich — der von der Karte angegebene Tintenbereich (x=324–440 bis y=210) war bereits korrekt; nur der Rendering-Bereich, eine bewusst konservative Untermenge davon, wurde verschoben.
