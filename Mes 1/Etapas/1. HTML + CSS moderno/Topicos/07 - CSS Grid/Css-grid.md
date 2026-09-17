# CSS Grid

## Grid Layout Module

O CSS Grid, como o próprio nome diz, oferece um layout baseado em grid para a página HTML baseado em linhas e colunas. A principal diferença do **CSS Grid** para o **Flex Box** são as dimenções, enquanto flex segue apenas uma direção, coluna ou linha, grid aplica ambas e isso é o que chamamos de duas dimensões.

Assim como o Flexbox, podemos dividir o Grid Layout em *Container* e *Item*, a lógica permanece a mesma.

## Grid Container

Um elemento se torna **Grid Container** quando a propriedade `display` é definida como `grid` ou `inline-grid`. O container pode conter um ou mais Items dentro dele, que se alinham em linhas e colunas.

#### grid

O `display: grid;` cria um container que se comporta como um bloco de duas dimensões que ocupa 100% da largura disponível por padrão forçando a quebra de linha e empurrando elementos próximos para a linha de baixo.

#### inline-grid

O `display: inline-grid` cria um container que se comporta como um elemento em linha, ocupando apenas o espaço necessário e permitindo que outros elementos compartilhem o mesmo espaço sem quebra de linha.

---

### Propriedades do Container

`align-content`

Alinha verticalmente os itens da grade dentro do contêiner.

`align-items`

Especifica o alinhamento padrão para itens dentro de um contêiner flexbox ou grid.

`display`

Especifica o comportamento de exibição (o tipo de caixa de renderização) de um elemento.

`column-gap`

Especifica o espaço entre as colunas.



`grid`

Uma atalho para as propriedades `grid-template-rows`, `grid-template-columns`, `grid-template-areas`, `grid-auto-rows`, `grid-auto-columns` e `grid-auto-flow`.


`grid-auto-columns`

Especifica um tamanho de coluna padrão.

`grid-auto-flow`

Especifica como os itens de posicionamento automático são inseridos na grade.

`grid-auto-row`

Especifica um tamanho de linha padrão.

`grid-template`

Uma atalho para as propriedades `grid-template-rows`, `grid-template-columns` e `grid-areas`


`justify-content`

Alinha horizontalmente os itens da grade dentro do container.

`place-content`

Uma propriedade abreviada para as propriedades align-content e justify-content.

`row-gap`

Especifica o espaçamento entre as linhas da grade.

#### Grid Gaps

`gap`

Uma atalho para as propriedades de espaçamento entre linhas e espaçamento entre colunas.

`column-gap`

somente espaçamento de colunas.

`row-gap`

somente espaçamento de linhas.

#### Grid Tracks

`grid-template-columns`

Especifica o tamanho das colunas e quantas colunas haverá em um layout de grade.

`grid-template-rows`

Especifica o tamanho das linhas em um layout de grade.

`grid-template-areas`

Especifica como exibir colunas e linhas, usando itens de grade nomeados.


---
---
---

## Grid Items