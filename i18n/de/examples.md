## Gearbeitete Karte — Clarendon Kleinbuchstaben `a`

Territorium: eine Glyphe, `ClarendonLTStd.otf`, zitiert 2026-08-21. Elf Karten leben in [`objects/`](objects/) — diese Datei ist der Katalog, keine Kopie von ihnen. Terminologie gegen das `typography-fundamentals`-Fertigkeitsglossar geprüft; zwei aus dem Gedächtnis entworfene Begriffe ("Bogen", "Schwanz") waren falsch und wurden ersetzt — siehe [`reference/decisions.md`](reference/decisions.md).

### Katalog

| Part | Typ | Status | Karte |
| ------------- | --------------- | ----------------- | -------------------------------------------------------- |
| Stem | Schlaganfall | Live  | [`objects/stem.md`](objects/stem.md)                      |
| Bowl | Schlaganfall | Live  | [`objects/bowl.md`](objects/bowl.md)                      |
| Finial | Schlaganfall | Live  | [`objects/finial.md`](objects/finial.md)                  |
| Kugelklemme | Stroke ending | Live  | [`objects/ball-terminal.md`](objects/ball-terminal.md)    |
| Spur | Stroke ending | Live  | [`objects/spur.md`](objects/spur.md)                      |
| Zähler | Negativraum | Live, derived | [`objects/counter.md`](objects/counter.md)                |
| Aperture | Negativraum | Live, derived | [`objects/aperture.md`](objects/aperture.md)              |
| x-Höhe | Metrisch | Live  | [`objects/x-height.md`](objects/x-height.md)              |
| Baseline | Metrisch | Live  | [`objects/baseline.md`](objects/baseline.md)              |
| Overshoot | Korrektur | Rest  | [`objects/overshoot.md`](objects/overshoot.md)            |
| Foot Serif | Schlaganfall | 👻 Geist | [`objects/foot-serif.md`](objects/foot-serif.md)          |

Ein Kaltleser hört hier auf, es sei denn, ein Teil muss geöffnet werden.

### Ein Spaziergang, in voller Länge

*Frage: "Ich möchte diesem Clarendon `a` einen schwereren Plattenfuß geben, der zum Rest des Gesichts passt, was berührt das?"*

1. Öffnen Sie den Katalog oben. „Foot serif“ ist die offensichtliche Tür.
2. Öffne `objects/foot-serif.md`. In der ersten Zeile des Textkörpers steht: Es gibt keine Fußserifen auf dieser Glyphe. Status: **ghost**.
3. Die Prämisse der Frage ist falsch — es gibt keine vorhandene Fußserife, die man schwerer machen könnte. Die Karte nennt auch die beiden echten Striche, die ein Leser stattdessen gemeint haben könnte: [`spur`](objects/spur.md) und [`ball-terminal`](objects/ball-terminal.md), und erklärt mit einem zitierten Koordinatenlauf, warum keiner von beiden eine Serife ist.

Um diese Frage zu beantworten, musste keine weitere Karte geöffnet werden, das ist der Sinn des Katalogs.

### Ein zweiter Spaziergang, kürzer

**Question:** "Was ist der Zähler, und kann ich ihn von alleine größer machen?"

1. Öffnen Sie `objects/counter.md`.
2. **Hits**: Nichts direkt — es ist von `bowl` und `stem` abgeleitet.
3. **Does not hit**: Mit der Blende meinen die Leute meistens eine separate weiße Form.
4. Antwort: Nein, nicht von alleine. Editieren Sie `bowl` oder `stem`; der Zähler folgt.

### Ein dritter Spaziergang, über den Wortschatz selbst

**Question:** "Wie heißt der Bogen auf diesem A?"

1. Es gibt keinen `arch.md`. Der Katalog enthält keine Zeile mit dem Namen "Arch".
2. `reference/naming-collisions.md` nennt genau diese Frage und verweist auf [`objects/finial.md`](objects/finial.md) – den Skill-basierten Begriff für diesen Buchstaben, mit dem Grund, dass „Bogen“ hier nicht zutrifft (er kehrt nie zur Basislinie zurück, also ist er keiner).
3. Stop, mit dem Wortschatz korrigiert, nicht nur die Geometrie gefunden.
