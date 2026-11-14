# Letterform Cartographer

Um mapa de sistema de um glifo: a letra minúscula **a** em Clarendon LT Std Onze cartas substantivas — nove vivas, uma sobra, um fantasma — cada uma citando um intervalo exato do contorno real da fonte, não uma aproximação redesenhada dele.

## Demonstração ao vivo

`docs/index.html` — um diagrama hoverable da carta. Cada hover busca e renderiza o card `.md` real de `objects/`, ao vivo, diretamente deste repositório. Nada no diagrama é uma cópia dos cards; é um visualizador sobre eles. Servi-lo a partir da raiz do repositório (GitHub Pages: fonte = `/ (root)`, não `/docs`) para que o fetch relativo de ZQx0 para `../objects/*.md` resolva — Páginas restritas apenas para ZQx5 teriam 404 em cada card.

## Por que isso existe

“Bowl”, “counter”, “spur” são nomes que um ser humano desenha em torno de intervalos desses dados — nada em um arquivo de fonte se rotula. Esse repositório é esse rotulagem, feito uma vez, citado contra o esboço real extraído (`fontTools`) e uma habilidade de referência tipográfica carregada, para que ninguém tenha que re-derivá-lo a olho nu.

## O único fantasma, explicado na frente

Clarendon is a slab serif — that's the first and often only thing anyone knows about it, and it creates a confident, wrong expectation: that every stroke in the face ends in a bracketed slab foot. This lowercase `a` doesn't. Its stem ends in a curved spur, its finial ends in a ball terminal, and no foot serif exists anywhere on the letter. That's not a simplification or an artistic choice being described loosely — it's a fact about the actual outline, verified against a second independent Clarendon after the first extraction was nearly discarded as corrupt for lacking the very serif this README just told you not to expect. See [`objects/foot-serif.md`](objects/foot-serif.md) for the full account.

## Como um estranho — ou uma sessão fria de IA — usa isso

1. Leia `identity.md` e `rules.md` uma vez. Eles são curtos.
2. Abra `examples.md`. É uma tabela de catálogo de todas as onze peças mais três caminhadas curtas trabalhadas.
3. Precisa de uma peça? Abra exatamente o cartão em `objects/`. Pare por aí.
4. Se você acertar um nome que não está no catálogo ("arch", "tail")? Verifique `reference/naming-collisions.md` primeiro. É muito provável que ele já tenha sido respondido.

**The one rule: load the catalog, then one card. Never all eleven at once.**

## O que está aqui

| Caminho | Trabalho |
| --- | --- |
| `identity.md` | Quem é o cartógrafo, de quem é o território, quem é o leitor posterior |
| `rules.md` | O que conta como um substantivo aqui, como Live/Leftover/Ghost são decididos, a regra Hits/Does-not-hit |
| `examples.md` | A tabela do catálogo + três caminhadas trabalhadas, datada de 2026-08-21 |
| `objects/` | As onze cartas em si — as prateleiras reais |
| `reference/card-types.md` | As três formas de cartas que este território usa |
| `reference/naming-collisions.md` | Quatro verdadeiras armadilhas de vocabulário, escritas uma vez |
| `reference/decisions.md` | Decisões registradas (escolha de fonte; correções de terminologia; técnica de renderização) com justificativa |
| `docs/index.html` | O diagrama ao vivo — um visualizador sobre `objects/`, não uma cópia dele |

## O que isto não é

Not a font-design tutorial, not an audit of Clarendon, not a copy of the glyph's data in nicer prose. If a card and the real outline in `ClarendonLTStd.otf` ever disagree, the outline is right and the card is wrong — every numeric claim in `objects/` cites a contour point range or a font table value specifically so that check is possible.

## Território e sourcing

- Fonte: Clarendon LT Std Roman (`ClarendonLTStd.otf`, Adobe), verificada contra um segundo Clarendon independente antes do uso — veja `reference/decisions.md`.
- Terminologia: habilidade `typography-fundamentals` (glossário, notas de contraforma, referência de classificação).Dois termos elaborados de memória antes dessa auditoria (“arco”, “cauda”) estavam errados e foram substituídos pelos termos reais da habilidade (“finial”, “esporão”).
- O diagrama descreve o glifo e onze palavras de rótulo como caminhos vetoriais em vez de incorporar Clarendon ou Akzidenz-Grotesk como fontes web — ambos são softwares de fontes comerciais; apenas as formas de letras específicas usadas como arte do diagrama são enviadas, não as próprias fontes.O texto do corpo do cartão (que é prosa sem limites, não uma lista fixa de palavras) usa uma pilha de fontes CSS do sistema — Helvetica Neue, voltando para Helvetica, Arial e sans-serif — então ele não envia nenhum arquivo de fonte de qualquer maneira.

Construído seguindo a sexta forma descrita no Weekly Comp #11: The Cartographer — um mapa de sistema de um corpo de trabalho real e em vigor, usando os invariantes da habilidade ICM Architect (github.com/RinDig/icm-architect) como andaimes.
