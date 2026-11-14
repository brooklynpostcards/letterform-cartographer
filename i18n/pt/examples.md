## Mapa trabalhado — Clarendon minúsculo `a`

Território: um glifo, `ClarendonLTStd.otf`, citado em 2026-08-21. Onze cards vivem em [`objects/`](objects/) — este arquivo é o catálogo, não uma cópia deles. Terminologia auditada contra o glossário de habilidades de `typography-fundamentals`; dois termos elaborados de memória (“arco”, “cauda”) estavam errados e foram substituídos — veja [`reference/decisions.md`](reference/decisions.md).

### Catálogo

| Parte | Tipo | Estado | Cartão |
| ------------- | --------------- | ----------------- | -------------------------------------------------------- |
| Cabeça | Acidente vascular cerebral | Ao vivo | [`objects/stem.md`](objects/stem.md)                      |
| Taça | Acidente vascular cerebral | Ao vivo | [`objects/bowl.md`](objects/bowl.md)                      |
| Final | Acidente vascular cerebral | Ao vivo | [`objects/finial.md`](objects/finial.md)                  |
| Terminal de esfera | terminação do acidente vascular cerebral | Ao vivo | [`objects/ball-terminal.md`](objects/ball-terminal.md)    |
| Rastrear | terminação do acidente vascular cerebral | Ao vivo | [`objects/spur.md`](objects/spur.md)                      |
| Contador | espaço negativo |   vivo, derivado | [`objects/counter.md`](objects/counter.md)                |
| Abertura | espaço negativo |   vivo, derivado | [`objects/aperture.md`](objects/aperture.md)              |
| x-altura | métrica | Ao vivo | [`objects/x-height.md`](objects/x-height.md)              |
| Linha de base | métrica | Ao vivo | [`objects/baseline.md`](objects/baseline.md)              |
| Excesso | correção | Restos | [`objects/overshoot.md`](objects/overshoot.md)            |
| Foot serif | Acidente vascular cerebral | 👻 fantasma | [`objects/foot-serif.md`](objects/foot-serif.md)          |

Um leitor frio pára aqui, a menos que uma parte precise ser aberta.

### Uma caminhada, na íntegra

*Pergunta: "Eu quero dar a este Clarendon `a` um pé de laje mais pesado para combinar com o resto do rosto.O que isso toca?"*

1. Abra o catálogo acima. “Foot serif” é a porta óbvia.
2. Abra `objects/foot-serif.md`. Ele diz, na primeira linha do corpo do texto: não há serif de pé neste glifo. Status: **ghost**.
3. A premissa da pergunta está errada — não há nenhuma serif de pé existente para tornar mais pesada. O cartão também nomeia os dois traços reais que um leitor poderia ter querido em vez disso: [`spur`](objects/spur.md) e [`ball-terminal`](objects/ball-terminal.md), e explica, com uma coordenada citada, por que nenhum deles é uma serif.

Nenhum outro cartão teve que ser aberto para responder a isso, esse é o ponto do catálogo.

### Uma segunda caminhada, mais curta

**Question:** "O que é o balcão, e posso torná-lo maior por conta própria?"

1. Abra o `objects/counter.md`.
2. **Hits**: nada diretamente — é derivado de `bowl` e `stem`.
3. **Does not hit**: a abertura, uma forma branca separada que as pessoas geralmente querem dizer em vez disso.
4. Resposta: não, não sozinho. Edite `bowl` ou `stem`; o contador segue. Pare.

### Uma terceira caminhada, sobre o próprio vocabulário

**Question:** "O que é o arco chamado sobre este a?"

1. Não há nenhum `arch.md`. O catálogo não tem nenhuma linha chamada "Arch".
2. `reference/naming-collisions.md` nomeia essa pergunta exata e aponta para [`objects/finial.md`](objects/finial.md) — o termo baseado em habilidade para essa carta, com a razão de que "arco" não se aplica aqui (ele nunca retorna à linha de base, então não é um).
3. Pare, com o vocabulário corrigido, não apenas a geometria localizada.
