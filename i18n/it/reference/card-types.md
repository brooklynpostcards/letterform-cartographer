## Tipi di carte (set chiuso)

Esistono tre tipi di carte in questo territorio.

### Corsa / fine corsa

Campi obbligatori: cosa è (una riga, indicando il termine definito dall'abilità), stato con intervallo di punti citato, colpisce, non colpisce.

### Spazio negativo (derivato)

Una forma delimitata da tratti senza contorni propri — il contatore, l’apertura. I campi richiesti sono gli stessi, ma “hits” per questi è quasi sempre “niente direttamente” — una forma derivata non ha geometria da modificare, solo tratti che la delimitano.

### Metrico

Questi citano le tabelle del font stesso (`OS/2`, `hhea`) piuttosto che il contorno, e la loro linea “hits” nomina ogni glifo nel font, non solo questo — l'unico punto in questo territorio dove il raggio di esplosione di una carta lascia la lettera.

## Il fantasma non è un quarto tipo

`foot-serif.md` usa il modello Stroke con `status: ghost`: un fantasma non prende una forma propria, ma la forma che il lettore si aspetta, piena della scoperta che non c’è niente.

## Se si presenta una dodicesima parte

Solo se il contorno stesso cambia (un peso diverso, un glifo ridisegnato) — una nuova carta segue uno dei tre modelli sopra e viene aggiunta alla tabella del catalogo in `examples.md`.
