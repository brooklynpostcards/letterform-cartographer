## Kartenarten (geschlossener Satz)

In diesem Gebiet gibt es drei Kartentypen.

### Hub / Hubende

Erforderliche Felder: was es ist (eine Zeile, Bezeichnung des Skill-definierten Begriffs), Status mit angegebenem Punktbereich, Treffer, trifft nicht.

### Negativer Raum (abgeleitet)

Eine Form, die durch Striche ohne eigene Kontur begrenzt ist – der Zähler, die Blende. Die erforderlichen Felder sind die gleichen, aber „Treffer“ für diese sind fast immer „nichts direkt“. Eine abgeleitete Form hat keine Geometrie zum Bearbeiten, nur Striche, die sie begrenzen.

### Metrisches System

Eine Schriftbreite Referenzlinie, nicht Teil der eigenen Glyphenkontur — x-height, baseline, overshoot. Diese zitieren die eigenen Tabellen der Schrift (`OS/2`, `hhea`) anstatt der Kontur. Ihre „Hit“-Zeile nennt jede Glyphe in der Schrift, nicht nur diese — die einzige Stelle in diesem Gebiet, an der der Blasenradius einer Karte den Buchstaben verlässt.

## Der Geist ist kein vierter Typ

`foot-serif.md` verwendet die Stroke-Vorlage mit `status: ghost`: Ein Geist bekommt nicht seine eigene Form – er bekommt die Form, die der Leser erwartet, gefüllt mit der Feststellung, dass nichts da ist.

## Wenn ein zwölfter Teil auftaucht

Nur wenn sich der Umriss selbst ändert (eine andere Stärke, eine neu gezeichnete Glyphe) — folgt eine neue Karte einer der drei oben genannten Vorlagen und wird in die Katalogtabelle in `examples.md` hinzugefügt.`examples.md` bleibt ansonsten ein datierter Schnappschuss.
