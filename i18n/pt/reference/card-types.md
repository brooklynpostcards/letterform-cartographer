## Tipos de cartões (conjunto fechado)

Existem três tipos de cartões neste território.

### Curso / curso-terminação

Campos obrigatórios: o que é (uma linha, nomeando o termo definido pela habilidade), status com o intervalo de pontos citado, acertos, não acerta.

### Espaço negativo (derivado)

Uma forma delimitada por traços sem contorno próprio — o contador, a abertura. Os campos necessários são os mesmos, mas “hits” para estes é quase sempre “nada diretamente” — uma forma derivada não tem geometria para editar, apenas traços que a limitam.

### Métrico

Uma linha de referência com a largura da fonte, não parte do próprio contorno do glifo — x-height, baseline, overshoot. Essas linhas citam as próprias tabelas da fonte (`OS/2`, `hhea`) ao invés do contorno. Sua linha de "hits" nomeia cada glifo na fonte, não apenas este — o único lugar nesse território onde o raio de explosão de um card deixa a letra.

## O fantasma não é um quarto tipo

`foot-serif.md` usa o modelo Stroke com `status: ghost`.Um fantasma não recebe sua própria forma — ele recebe a forma que o leitor esperava, cheio com a descoberta de que nada está lá.

## Se uma décima segunda parte aparecer

Somente se o esboço em si mudar (um peso diferente, um glifo redesenhado) — um novo card segue um dos três modelos acima e é adicionado à tabela de catálogo em `examples.md`.`examples.md` permanece um instantâneo datado caso contrário.
