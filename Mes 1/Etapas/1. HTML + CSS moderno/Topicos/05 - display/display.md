# CSS Display

É uma propriedade que se encontra presente nas tags HTML, como ela é possível definir o comportamento das caixas de renderização do elemento na página. Os principais valores para essa propriedade são: `block`, `inline`, `inline-block`, `flex`, `grid` e `none`.


### Valores

`block`

Com essa propriedade o elemento ocupa toda a largura da linha e também força a quebra de linha antes e depois dele mesmo, sendo uma propriedade muito útil quando deve se poscionar apenas um elemento em um determinado espaço horizontal da página.

`inline`

É o oposto de block, com o inline o elemento ocupa apenas o espaço que precisa na linha e fica lado a lado com outros elementos na mesma linha.

`inline-block`

Essa propriedade une os conceitos de **inline** e **block**, permitindo que o elemento possua largura e altura como um bloco mas flua na linha como um inline. Perceba que no exemplo em `index.html` o paragrafo 1 e 2 estão na mesma linha e cada um com a mesma propriedade de um bloco, chamo atenção para o detalhe de que eles só estão na mesma linha devido ao seu tamanho não excede-la, você pode testar o comportamento abrindo o Dev Tools e diminuindo o tamanho da View Box da página.

`flex`

O flex aplicado a um container permite que o elemento se comporte de maneira flexivel em uma direção, que podem ser `column` para alinhamento vertical ou `row` para horizontal. Esse propriedade é muito util quando queremos criar páginas responsivas para nossos sites.

`grid`

O grid cria um layout em grade com linhas e colunas, muito util quando se quer posicionar diversos elementos, como cards por exemplo. Podemos utilizar `grid-template-rows` e `grid-template-columns` para definir o tamanho de linhas e colunas.

````CSS
    .grid {
        display: grid;
        grid-template-columns: 200px 200px;
        grid-template-rows: 100px 200px;
        gap: 10px;
    }
````

No código acima cada valor em `grid-template-columns` define a largura de uma coluna, a quantidade de valores dentro da propriedade define a quantidade de colunas mas podemos utilizar valores que automatizam as colunas, o mesmo raciocinio pode ser aplicado para as linhas.

`none`

Esconde o elemento e o remove do layout, pode usar essa opção com manipulação do DOM para ocultar elementos, no arquivo index.html há um exemplo de como fazer isso com javascript.