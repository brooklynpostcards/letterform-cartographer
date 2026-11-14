## Was zählt als Substantiv

Ein **anatomical part**: ein benannter Bereich des Glyphenumrisses oder eine benannte Schriftbreiten-Referenzlinie, an der der Umriß gemessen wird.In diesem Gebiet existieren elf - neun lebend, ein Überrest, ein Geist.

Zwei Arten von Substantiven:

- **Stroke parts** (Schaft, Schale, Endstück, Kugelkopf, Sporn) — ein zusammenhängender Abschnitt der äußeren Kontur.
- **Derived shapes** (Zähler, Öffnung) — Weißraum, der von Strichteilen begrenzt ist, die keine eigene Kontur haben.
- **Metrics** (x-height, baseline, overshoot) — horizontale Referenzlinien aus den Tabellen der Schriftart, überhaupt nicht die Kontur der Glyphe.

## Was als Bewegung zählt

Das Bearbeiten eines Strichteils ändert den Umrissbereich, den es benennt, und alles, was strukturell an den Bereich grenzt. Ein Stamm, der eine Kante mit dem Zähler teilt, bedeutet, dass die Verbreiterung des Stamms den Zähler verengt - das ist ein echter Hit, zitieren Sie ihn. Ein Stamme, der nichts mit der x-Höhe teilt, heißt, dass die Änderung des Stammes ihn nie berührt - das ist eine echte Missachtung, zitieren sie auch.

Metriken bewegen sich anders: Sie treffen *jede Glyphe in der Schriftart*, niemals nur diese.Diese Asymmetrie – eine Strichänderung einer Glyphe bleibt lokal, eine Schriftart-weite Metrikänderung wird global – ist das Wichtigste, was eine Karte in diesem Gebiet richtig machen kann.

## Live / Rest / Ghost, definiert für dieses Gebiet

- **Live** — Das Teil entspricht einem realen Bereich der tatsächlichen Kontur, zitierbar durch Punktindex und Koordinate.
- **Leftover** — Das Teil ist real und gegenwärtig, aber seine Existenzgrundlage ist eine Korrektur einer früheren Designtradition, nicht ein Merkmal dieser Glyphe an sich.Der Überschuss: er tut immer noch seine Arbeit, ist immer noch erklärenswert, nicht etwas, das "repariert" werden muss.
- **Ghost** — Der Geist dieses Gebietes, die Fußserife, existiert eben deshalb, weil die eigene Kategorie der Schrift (Slab Serif) eine Erwartung setzt, die dieser Buchstabe nicht erfüllt, und die Fußserie gibt es nur, weil sie in einer bestimmten Schriftart verwendet wird.

## Treffer / Trifft nicht

Jede Karte endet mit genau zwei Zeilen: **Hits** bezeichnet den echten strukturellen Nachbarn, **Does not hit** den falschen Nachbarn – normalerweise den Teil, der in der gerenderten Buchstabenform angrenzend erscheint, aber in den Umrissdaten keine tatsächliche Grenze teilt.

## Ablehnungen

- Kein Einfügen der Rohpfaddaten der Glyphe in eine Karte, als ob dies eine Erklärung wäre - Punktbereiche und Grenzen zitieren, dieselbe Disziplin wie das Zitieren eines Dateipfads anstelle des Einfügens eines Skripts.
- Keine Behandlung einer abgeleiteten Form (Zähler, Öffnung), als ob sie unabhängige Geometrie zum Bearbeiten hätte.
- Ein Teil, der nicht existiert, bekommt eine Karte, die es sagt, nicht Stillschweigen.

## Wie eine Karte aufgebaut wird

Bevor man eine Karte schreibt, sollte man die eigentliche Umrisse extrahieren (`fontTools`, nicht ein gerendertes Bild, nicht eine Erinnerung daran, wie Clarendon „aussehen sollte“), den Punktbereich identifizieren, den das Teil einnimmt, und es mit einer zweiten unabhängigen Quelle der gleichen Schrift überprüfen, bevor man etwas vertraut, das überraschend aussieht.Die Geisterkarte dieses Territoriums existiert, weil diese Überprüfung notwendig war - der erste Blick auf die Umrisse schien genau dort falsch zu sein, wo sie tatsächlich richtig waren.
