# Flexbox

Vimos no tópico anterior que podemos configurar a propriedade display de um elemento como `flex`, isso é só a ponta de um *iceberg* chamado ***Flexbox***.

Flexbox é todo assunto a respeito do flex, assim como o ***CSS Grid*** é para a propriedade `display: grid`.

## Flex Container e Flex Item

Podemos dividir o Flexbox em dois elementos principais que formam um componente flex, são eles o **Flex Container** e o **Flex Item**. Como você pode imaginar o Flex Container é o elemento que abraça todo o conteudo onde o flex é aplicado, ele é quem recebe a popriedade `display:flex` e automaticamente tudo aquilo que está dentro dele se torna um Flex Item.


## Flex Container

Como eu disse, o Flex Containerse trata de um elemento que recebe outros elementos e possui o comportamento flex. A seguir vou listar algumas de suas propriedades CSS.

### Propriedades
`display`

Essa ja vimos, ela é a propriedade que usamos para aplicar o "Flex Behavior", para isso basta defini-la com o valor `flex`.

````CSS
    section {
        display: flex;
    }
````

`flex-direction`

Assim como display, *flex-direction* é essencial para o funcionamento do flex, é ela quem define se vamos alinhas os Flex Item's horizontal ou verticalmente, usamos `column` e `row` para isso. Além disso podemos adicionar o `-reverse`, que serve para definirmos o ponto de origem do alinhamento para o contrario do padrão.

Para alinhar os Flex Items em uma coluna:
````CSS
    section {
        display: flex;
        flex-direction: column;
    }
````

Para alinhar os Flex Items em uma coluna de baixo para cima:
````CSS
    section {
        display: flex;
        flex-direction: column-reverse;
    }
````

A mesma lógica se aplica a `flex-direction: row;`.

>Por padrão o valor dessa propriedade é `row`

`flex-wrap`

Essa propriedade determina se o componente deve ou não haver quebra de linha quando todos os itens não couberem na linha. Por padrão seu valor é `nowrap` o que faz com que os itens se redimensionem para que caibam no espaço da linha. O flex-wrap pode usar o `-reverse` em seu valor também.

````CSS
    section {
        display: flex;
        flex-direction: row;
        flex-wrap: wrap-reverse;
    }
````

`flex-flow`

Essa é uma maneira de você definir `flex-direction` e `flex-wrap` em uma propriedade só, da seguinte maneira:

````CSS
    section{
        display: flex;
        flex-flow: row wrap;
    }
````

`justify-content`

Podemos usar os valores dessa propriedade para usar o espaço horizontal interno do container para alinhar os itens. Os valores são:

***center*** : mantem o(s) item(ns) no centro do container.

***flex-start*** : posiciona no começo do container, ou seja, o lado esquerdo.

***flex-end*** : posiciona no fim do container.

***space-around*** : dispoe os itens de forma que todo o espaço disponivel fique em volta.

***space-between*** : dispoe os itens de forma que todo o espaço fique entre um item e outro apenas.

***space-evenly*** : dispoe os itens de forma que o espaço seja igualmente distribuido entre eles.

`align-items`

Diferente da anterior, essa propriedade é responsavel pelo alinhamento vertical dos itens. Os valores são:

***normal*** : é o valor padrão, possui o mesmo efeito de **stretch**.

***stretch*** : estica os itens de modo que cubram todo o espaço vertical do container.

***center*** : alinha os itens no meio do container.

***flex-start*** : alinha os itens no topo do container.

***flex-end*** : alinha os itens no fundo do container.

***baseline*** : faz o alinhamento do itens deixando os textos na mesma altura.

`align-content`

Serve para alinhar as linhas da pagina, mas somente se o `flex-wrap` estiver com o valor `wrap` fazendo a quebra de linha.

Possui os mesmos valores de `justify-content` só que desta vez sendo aplicado nas "linhas".

## Flex Items

Como vimos anteriormente, todo elemento que está diretamente dentro de um **Flex Container** automaticamente se torna um **Flex Item**.

### Propriedades

`order`

Define a ordem em que os Flex Items aparecem dentro do container.

Por padrão o valor é `0`, e quanto menor o valor, mais cedo o item aparece.

```CSS
.item {
    order: 2;
}
```

`flex-grow`

Define quanto um Flex Item pode crescer em relação aos outros quando existe espaço disponível.

Por padrão o valor é `0`.

```CSS
.item {
    flex-grow: 2;
}
```

`flex-shrink`

Define quanto um Flex Item pode diminuir em relação aos outros quando não existe espaço suficiente.

Por padrão o valor é `1`.

```CSS
.item {
    flex-shrink: 2;
}
```

`flex-basis`

Define o tamanho inicial de um Flex Item.

```CSS
.item {
    flex-basis: 250px;
}
```

`flex`

É uma forma abreviada de definir `flex-grow`, `flex-shrink` e `flex-basis` em uma única propriedade.

```CSS
.item {
    flex: 1 0 150px;
}
```

Nesse exemplo:

```text
flex-grow: 1
flex-shrink: 0
flex-basis: 150px
```

`align-self`

Define o alinhamento de um Flex Item individualmente, sobrescrevendo o valor definido por `align-items` no Flex Container.

```CSS
.item {
    align-self: center;
}
```

Podemos também definir diferentes alinhamentos para cada item:

```CSS
.item-2 {
    align-self: flex-start;
}

.item-3 {
    align-self: flex-end;
}
```