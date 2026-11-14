# Letterform Cartographer

Eine Systemkarte einer Glyphe: der Kleinbuchstabe **a** in Clarendon LT Std Roman.Elf Substantivkarten — neun lebend, eine übrig, eine Geist — jede zitiert einen exakten Bereich der tatsächlichen Schriftkontur, nicht eine neu gezeichnete Näherung davon.

## Live-Demo

`docs/index.html` — ein hoverbares Diagramm des Buchstabens. Jeder Hover holt und rendert die tatsächliche `.md`-Karte aus `objects/`, live, direkt aus diesem Repository. Nichts im Diagramm ist eine Kopie der Karten; es ist ein Betrachter über ihnen. Stellen Sie es aus dem Repository-Wurzel (GitHub Pages: Quelle = `/ (root)`, nicht `/docs`) bereit, so dass der relative Fetch zu `../objects/*.md` auflöst — Seiten, die nur auf ZQX7 beschränkt sind, würden auf jeder Karte 404 anzeigen.

## Warum das existiert

Ein Glyphen-Outline ist nur eine Punktkoordinate. „Bowl“, „counter“, „spur“ sind Namen, die ein Mensch um Bereiche dieser Daten zieht – nichts in einer Schriftdatei beschriftet sich selbst. Dieses Repository ist diese Beschriftung, die einmal durchgeführt wurde und sowohl gegen den wirklich extrahierten Outline (`fontTools`) als auch gegen eine geladene Typografie-Referenz-Fähigkeit zitiert wird, so dass niemand sie mit dem Auge neu ableiten muss.

## Der eine Geist, erklärt von vorne

Clarendon ist eine Slab-Serif — das ist das erste und oft das einzige, was jemand über sie weiß, und es erzeugt eine selbstbewusste, falsche Erwartung: dass jeder Strich in der Fläche in einem eingeklammerten Slab-Fuß endet. Diese Kleinbuchstabe `a` tut es nicht. Ihr Stamm endet in einem gebogenen Sporn, ihr Endstück in einem Kugelende, und es gibt nirgendwo auf dem Buchstaben eine Fuß-Serif. Das ist keine Vereinfachung oder eine künstlerische Wahl, die locker beschrieben wird — es ist eine Tatsache über die tatsächliche Umrisse, überprüft gegen eine zweite unabhängige ZQx1, nachdem die erste Extraktion beinahe als beschädigt verworfen wurde, weil sie genau die Serife fehlte, von der diese README gerade sagte, dass man sie nicht erwarten sollte. Siehe [`objects/foot-serif.md`](objects/foot-serif.md) für die vollständige Beschreibung.

## Wie ein Fremder – oder eine kalte KI-Sitzung – dies nutzt

1. Lesen Sie `identity.md` und `rules.md` einmal. Sie sind kurz.
2. Öffne `examples.md`, es ist eine Katalogtabelle mit allen elf Teilen plus drei kurzen bearbeiteten Spaziergängen.
3. Benötigen Sie ein Teil? Öffnen Sie genau seine Karte in `objects/`.
4. Wenn du einen Namen findest, der nicht im Katalog steht („arch“, „tail“), schaue zuerst bei `reference/naming-collisions.md` nach — es ist sehr wahrscheinlich bereits beantwortet.

**The one rule: load the catalog, then one card. Never all eleven at once.**

## Was ist hier?

| Pfad | Job |
| --- | --- |
| `identity.md` | Wer der Kartograph ist, wessen Territorium das ist, wer der spätere Leser ist |
| `rules.md` | Was hier als Substantiv zählt, wie Live/Leftover/Ghost entschieden werden, die Hits/Does-not-hit-Regel |
| `examples.md` | Der Katalogtisch + drei bearbeitete Wanderungen, datiert 2026-08-21 |
| `objects/` | Die elf Karten selbst — die eigentlichen Regale |
| `reference/card-types.md` | Die drei Kartenformen, die dieses Gebiet verwendet |
| `reference/naming-collisions.md` | Vier echte Vokabelfallen, einmal aufgeschrieben |
| `reference/decisions.md` | Protokollierte Entscheidungen (Schriftartwahl; Terminologiekorrekturen; Rendertechnik) mit Begründung |
| `docs/index.html` | Das Live-Diagramm — ein Viewer über `objects/`, keine Kopie davon |

## Was das nicht ist

Not a font-design tutorial, not an audit of Clarendon, not a copy of the glyph's data in nicer prose. If a card and the real outline in `ClarendonLTStd.otf` ever disagree, the outline is right and the card is wrong — every numeric claim in `objects/` cites a contour point range or a font table value specifically so that check is possible.

## Territorium und Beschaffung

- Schriftart: Clarendon LT Std Roman (`ClarendonLTStd.otf`, Adobe), vor der Verwendung mit einem zweiten unabhängigen Clarendon überprüft — siehe `reference/decisions.md`.
- Terminologie: `typography-fundamentals`-Fertigkeit (Glossar, Gegenform-Hinweise, Klassifikationsreferenz) Zwei Begriffe, die vor diesem Audit aus dem Gedächtnis entworfen wurden („Bogen“, „Schwanz“), waren falsch und wurden durch die tatsächlichen Begriffe der Fertigkeit ersetzt („Final“, „Spur“).
- Das Diagramm umreißt die Glyphe und die elf Beschriftungswörter als Vektorpfade, anstatt entweder Clarendon oder Akzidenz-Grotesk als Webfonts einzubetten – beide sind kommerzielle Schriftsoftware; nur die spezifischen Buchstabenformen, die als Diagrammgrafik verwendet werden, werden geliefert, nicht die Schriften selbst. Der Kartenkörpertext (der unbegrenzte Prosa ist, keine feste Wortliste) verwendet einen System-CSS-Schriftartstapel – Helvetica Neue, der auf Helvetica, Arial und Sans-Serif zurückfällt – also wird keine Schriftartdatei in beiden Fällen geliefert.

Erstellt nach der sechsten Form, die in Weekly Comp #11 beschrieben wurde: The Cartographer — eine Systemkarte eines realen, in Kraft befindlichen Werkkörpers, der die Invarianten des ICM Architect Skills (github.com/RinDig/icm-architect) als Gerüst verwendet.
