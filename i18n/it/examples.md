## Mappa lavorata — Clarendon minuscolo `a`

Territorio: un glifo, `ClarendonLTStd.otf`, citato il 21-08-2026. Undici carte vivono in [`objects/`](objects/) — questo file è il catalogo, non una copia di esse. Terminologia controllata contro il glossario delle abilità di `typography-fundamentals`; due termini redatti da memoria (“arco”, “coda”) erano sbagliati e sostituiti — vedi [`reference/decisions.md`](reference/decisions.md).

### Catalogo

| Parte | Tipo | Stato | Carta |
| ------------- | --------------- | ----------------- | -------------------------------------------------------- |
| Voce | ictus | Livello | [`objects/stem.md`](objects/stem.md)                      |
| Ciotola | ictus | Livello | [`objects/bowl.md`](objects/bowl.md)                      |
| Finial | ictus | Livello | [`objects/finial.md`](objects/finial.md)                  |
| Terminale a sfera | Terminazione del colpo | Livello | [`objects/ball-terminal.md`](objects/ball-terminal.md)    |
| Traccia | Terminazione del colpo | Livello | [`objects/spur.md`](objects/spur.md)                      |
| Contatore | Spazio negativo | Live, derivato | [`objects/counter.md`](objects/counter.md)                |
| Apertura | Spazio negativo | Live, derivato | [`objects/aperture.md`](objects/aperture.md)              |
| x-altezza | metrica | Livello | [`objects/x-height.md`](objects/x-height.md)              |
| Baseline | metrica | Livello | [`objects/baseline.md`](objects/baseline.md)              |
| Overshoot | correzione | Resto | [`objects/overshoot.md`](objects/overshoot.md)            |
| Foot serif | ictus | 👻 fantasma | [`objects/foot-serif.md`](objects/foot-serif.md)          |

Un lettore a freddo si ferma qui a meno che una parte debba essere aperta.

### Una passeggiata, in pieno

*Domanda: "Voglio dare a questo Clarendon `a` un piede di lastra più pesante per abbinare il resto della faccia, cosa tocca?"*

1. Apri il catalogo qui sopra. “Foot serif” è la porta ovvia.
2. Apri `objects/foot-serif.md`. Dice, nella prima riga del corpo del testo: non c'è foot serif su questo glifo. Stato: **ghost**.
3. La premessa della domanda è sbagliata — non esiste un foot serif esistente da rendere più pesante. La scheda nomina anche i due tratti reali che un lettore avrebbe potuto intendere invece: [`spur`](objects/spur.md) e [`ball-terminal`](objects/ball-terminal.md), e spiega, con un passo di coordinate citato, perché nessuno dei due è un serif.

Nessun'altra carta doveva essere aperta per rispondere a questa domanda, questo è lo scopo del catalogo.

### Una seconda passeggiata, più breve

**Question:** "Qual è il bancone, e posso renderlo più grande da solo?"

1. Apri `objects/counter.md`.
2. **Hits**: Nulla direttamente — è derivato da `bowl` e `stem`.
3. **Does not hit**: L'apertura, una forma bianca separata che la gente di solito intende invece.
4. Risposta: no, non da solo. Modifica `bowl` o `stem`; il contatore segue. Stop.

### Una terza passeggiata, sul vocabolario stesso

**Question:** "Come si chiama l'arco su questo a?"

1. Non esiste `arch.md`. Il catalogo non ha alcuna riga denominata "Arch".
2. `reference/naming-collisions.md` dà il nome esatto a questa domanda e punta a [`objects/finial.md`](objects/finial.md) — il termine basato sull'abilità per questa lettera, con la ragione per cui "arco" non si applica qui (non ritorna mai alla linea di base, quindi non è uno).
3. Stop, con il vocabolario corretto, non solo la geometria localizzata.
