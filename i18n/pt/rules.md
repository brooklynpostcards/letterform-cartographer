## O que conta como um substantivo

Um **anatomical part**: um intervalo nomeado do contorno do glifo, ou uma linha de referência de largura de fonte nomeada contra a qual o contorno é medido.Existem onze neste território - nove vivos, um sobrando, um fantasma.

Dois tipos de substantivo:

- **Stroke parts** (haste, taça, terminais, terminal esférico, esporão) — um trecho contíguo do contorno externo.
- **Derived shapes** (contador, abertura) — espaço em branco delimitado por partes de traçado, sem contorno próprio.
- **Metrics** (x-height, baseline, overshoot) — linhas de referência horizontais das próprias tabelas da fonte, não o contorno do glifo.

## O que conta como movimento

Editar uma parte de traçado muda o intervalo de contorno que ele nomeia, e qualquer coisa que o intervalo estruturalmente limita. Um stem que compartilha uma borda com o contador significa que ampliar o stem estreita o contador — isso é um verdadeiro sucesso, cite-o. Um stem não compartilhando nada com a altura x significa que mudar o stem nunca toca nele — isso é uma verdadeira falha, cite-a também.

As métricas se movem de forma diferente: elas atingem *todos os glifos da fonte*, nunca apenas este. Essa assimetria — a mudança de traço de um glifo permanece local, uma mudança de métrica em toda a fonte se torna global — é a coisa mais importante que um card neste território pode acertar.

## Live / Leftover / Ghost, definido para este território

- **Live** — a peça corresponde a um intervalo real do contorno real, citável por índice de ponto e coordenada.
- **Leftover** — a parte é real e presente, mas sua razão de existir é uma correção de uma tradição de design anterior, não uma característica deste glifo por si só.O excesso: ainda fazendo seu trabalho, ainda vale a pena explicar, não algo para "consertar".
- **Ghost** — O fantasma desse território, a serif de pé, existe precisamente porque a própria categoria da fonte (slab serif) estabelece uma expectativa que essa letra não cumpre, e isso é algo que o leitor vai procurar, e não há nada por trás disso nesse glifo específico.

## Hits / Não acerta

Every card ends with exactly two lines. **Hits** names the real structural neighbor. **Does not hit** names the wrong neighbor a reader would guess first — usually the part that looks adjacent in the rendered letterform but shares no actual boundary in the outline data.

## Recusa

- Não cole os dados brutos do caminho do glifo em um cartão como se isso fosse uma explicação - cite intervalos de pontos e limites, a mesma disciplina de citar um caminho de arquivo em vez de colar um script.
- Não tratando uma forma derivada (contador, abertura) como se tivesse geometria independente para editar.
- Uma parte que não existe recebe um cartão que diz isso, não o silêncio.

## Como um cartão é construído

Antes de escrever qualquer cartão: extraia o contorno real (`fontTools`, não uma imagem renderizada, não uma memória do que Clarendon "deveria" parecer), identifique qual intervalo de pontos a parte ocupa e verifique-a contra uma segunda fonte independente da mesma fonte antes de confiar em qualquer coisa que pareça surpreendente.O cartão fantasma deste território existe porque essa verificação era necessária - a primeira olhada no contorno parecia errada exatamente onde estava correta.
