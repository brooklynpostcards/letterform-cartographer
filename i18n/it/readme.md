# Letterform Cartographer

Una mappa di sistema di un glifo: la lettera minuscola **a** in Clarendon LT Std Roman Undici carte sostantive — nove vive, una rimasta, una fantasma — ciascuna citando un intervallo esatto del contorno del carattere reale, non un'approssimazione ridisegnata di esso.

## Demo dal vivo

`docs/index.html` — un diagramma hoverable della lettera. Ogni hover recupera e renderizza la vera carta `.md` da `objects/`, live, direttamente da questo repository. Niente nel diagramma è una copia delle carte; è un visualizzatore su di esse. Servirlo dalla radice del repository (GitHub Pages: sorgente = `/ (root)`, non `/docs`) in modo che il fetch relativo di `../objects/*.md` a GitHub Pages si risolva — Le pagine limitate a ZQx5 da solo avrebbero 404 su ogni carta.

## Perché questo esiste

“Bowl”, “counter”, “spur” sono nomi che un essere umano disegna intorno a intervalli di quei dati — niente in un file di font etichetta se stesso. Questo repository è quell’etichettatura, fatta una volta, citata sia contro il vero outline estratto (`fontTools`) che contro una abilità di riferimento tipografico caricata, quindi nessuno deve ri-derivarlo a occhio.

## L'unico fantasma, spiegato in anticipo

Clarendon is a slab serif — that's the first and often only thing anyone knows about it, and it creates a confident, wrong expectation: that every stroke in the face ends in a bracketed slab foot. This lowercase `a` doesn't. Its stem ends in a curved spur, its finial ends in a ball terminal, and no foot serif exists anywhere on the letter. That's not a simplification or an artistic choice being described loosely — it's a fact about the actual outline, verified against a second independent Clarendon after the first extraction was nearly discarded as corrupt for lacking the very serif this README just told you not to expect. See [`objects/foot-serif.md`](objects/foot-serif.md) for the full account.

## Come uno sconosciuto — o una sessione fredda di IA — usa questo

1. Leggi `identity.md` e `rules.md` una volta, sono brevi.
2. Apri `examples.md`. È una tabella di catalogo di tutte le undici parti più tre brevi passeggiate lavorate.
3. Hai bisogno di una parte? Apri esattamente la sua scheda in `objects/`.
4. Se hai trovato un nome che non è nel catalogo ("arch", "tail") controlla prima `reference/naming-collisions.md` — molto probabilmente c'è già una risposta.

**The one rule: load the catalog, then one card. Never all eleven at once.**

## Cosa c'è qui

| Percorso | Lavoro |
| --- | --- |
| `identity.md` | Chi è il cartografo, di chi è il territorio, chi è il lettore successivo |
| `rules.md` | Che cosa conta come sostantivo qui, come Live/Leftover/Ghost sono decisi, la regola Hits/Does-not-hit |
| `examples.md` | La tavola del catalogo + tre passeggiate lavorate, datate 2026-08-21 |
| `objects/` | Le undici carte stesse — gli scaffali effettivi |
| `reference/card-types.md` | Le tre forme di carta che questo territorio utilizza |
| `reference/naming-collisions.md` | Quattro vere trappole del vocabolario, scritte una volta |
| `reference/decisions.md` | Decisioni registrate (scelta del font; correzioni terminologiche; tecnica di rendering) con motivazione |
| `docs/index.html` | Il diagramma dal vivo — un visualizzatore su `objects/`, non una copia di esso |

## Cosa questo non è

Not a font-design tutorial, not an audit of Clarendon, not a copy of the glyph's data in nicer prose. If a card and the real outline in `ClarendonLTStd.otf` ever disagree, the outline is right and the card is wrong — every numeric claim in `objects/` cites a contour point range or a font table value specifically so that check is possible.

## Territorio e sourcing

- Font: Clarendon LT Std Roman (`ClarendonLTStd.otf`, Adobe), verificato con un secondo Clarendon indipendente prima dell'uso — vedi `reference/decisions.md`.
- Terminologia: abilità `typography-fundamentals` (glossario, note sulla controforma, riferimento alla classificazione).Due termini elaborati a memoria prima di quell'audit ("arco", "coda") erano sbagliati e sono stati sostituiti con i termini effettivi dell'abilità ("finiale", "sperone").
- Il diagramma delinea il glifo e le undici parole dell'etichetta come percorsi vettoriali piuttosto che incorporare Clarendon o Akzidenz-Grotesk come font web — entrambi sono software di font commerciali; solo le forme di lettere specifiche utilizzate come grafica del diagramma vengono spedite, non i font stessi.Il testo del corpo della carta (che è prosa senza limiti, non un elenco fisso di parole) utilizza uno stack di font CSS di sistema — Helvetica Neue, ricadendo su Helvetica, Arial e sans-serif — quindi non spedisce alcun file di font in entrambi i modi.

Costruito seguendo la sesta forma descritta in Weekly Comp #11: The Cartographer — una mappa di sistema di un vero e proprio corpo di lavoro in vigore, utilizzando gli invarianti dell'abilità ICM Architect (github.com/RinDig/icm-architect) come impalcatura.
