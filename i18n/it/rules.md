## Cosa conta come sostantivo

Un **anatomical part**: un intervallo denominato del contorno del glifo, o una linea di riferimento denominata della larghezza del carattere rispetto alla quale il contorno viene misurato.

Due tipi di sostantivo:

- **Stroke parts** (stelo, coppa, terminale, terminale a sfera, sperone) — un tratto contiguo del contorno esterno.
- **Derived shapes** (contatore, apertura) — spazio bianco delimitato da parti del tratto, senza contorni propri.
- **Metrics** (x-height, baseline, overshoot) — linee di riferimento orizzontali dalle tabelle del font, non il contorno del glifo.

## Cosa conta come movimento

Modificare una parte di un tratto cambia l'intervallo di contorno che nomina, e qualsiasi cosa che confina strutturalmente con l'area. Uno stelo che condivide un bordo con il contatore significa che allargare lo stelo restringe il contatore — questo è un vero successo, citatelo.

Le metriche si muovono in modo diverso: colpiscono *ogni glifo del font*, mai solo questo.Questa asimmetria - un cambiamento di tratto di un glifo rimane locale, un cambiamento metrico a livello di font diventa globale- è la cosa più importante che una carta in questo territorio può fare bene.

## Live / Leftover / Ghost, definito per questo territorio

- **Live** — La parte corrisponde ad un intervallo reale del profilo effettivo, citabile per indice di punto e coordinata.
- **Leftover** — La parte è reale e presente, ma la sua ragione d'essere è una correzione di una precedente tradizione di design, non una caratteristica di questo glifo in sé.L'overshoot: ancora facendo il suo lavoro, ancora vale la pena di spiegare, non qualcosa da "riparare".
- **Ghost** — Il fantasma di questo territorio, il foot serif, esiste proprio perché la categoria del tipo di carattere (slab serif) stabilisce un'aspettativa che questa lettera non soddisfa, e questo è il motivo per cui la maggior parte dei tipi di carattere hanno un nome.

## Colpisce / Non colpisce

Ogni scheda termina con esattamente due righe. **Hits** nomina il vero vicino strutturale, mentre **Does not hit** nomina il vicino sbagliato che un lettore indovinerebbe per primo — di solito la parte che sembra adiacente nella forma di lettera renderizzata ma non condivide alcun confine effettivo nei dati di contorno.

## Rifiuti

- Non incollare i dati del percorso grezzo del glifo in una scheda come se fosse una spiegazione - citare intervalli di punti e confini, la stessa disciplina di citare un percorso di file invece di incollare uno script.
- Nessun trattamento di una forma derivata (contatore, apertura) come se avesse una geometria indipendente da modificare.
- Una parte che non esiste riceve una scheda che lo dice, non il silenzio.

## Come viene costruita una carta

Prima di scrivere qualsiasi scheda: estraete il vero contorno (`fontTools`, non un'immagine resa, non una memoria di come Clarendon "dovrebbe" apparire), identificate quale intervallo di punti occupa la parte, e controllatelo con una seconda fonte indipendente dello stesso carattere prima di fidarsi di qualsiasi cosa che sembri sorprendente.La carta fantasma di questo territorio esiste perché quel controllo era necessario - il primo sguardo al contorno sembrava sbagliato esattamente dove in realtà era giusto.
