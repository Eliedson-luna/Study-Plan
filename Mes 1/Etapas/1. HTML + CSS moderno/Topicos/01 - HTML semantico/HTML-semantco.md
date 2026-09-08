# O que é o HTML semantico?

Se trata de quando o nome das tags html descrevem sua função por si só. Por exemplo `section`, `main`, `nav` e por ai vai.

Exemplo: temos a tag `header` que podemos traduzir para "cabeçalho" e a partir dai temos uma ideia do que fazer com ela, basta pensarmos em quais as caracteristicas de um cabeçalho: posicionado no topo da página, possui menus de navegação...

Isso e diferente de outras tags que possuem nomes genéricos e que nem sempre dizem o que o elemento faz, como `div` ou `span`.  

<br>
<br>



# Exemplos de Elementos semânticos

`<article>`

especifica um conteúdo independente em uma página web, ou seja, deve fazer sentido por si só.

pode ser:
    Posts, Comentarios, Cards

---

`<aside>`

define um conteudo separado de onde está inserida

---

`<details>`

cria uma lista de detalhes retratil que o usuário pode abrir e fechar ao clicar

---

`<figcaption>`

usado junto à `<figure>` e `<img>` para definir uma legenda de uma imagem.

Exemplo:

```HTML
<figure>
    <img src="caminho/da/imagem">
    <figcaption> legenda da imagem aqui </figcaption>
</figure>
```

---

`<figure>`

como vimos no exemplo anterior, serve para criar um bloco de imagem, dentro podemos colocar uma imagem com <img> e uma legenda utilizando o <figcaption>

---
`<footer>`

é o rodapé da página, colocado abaixo de todos os elementos e contém informações úteis sobre a pagina como links, contatos, botões para voltar ao topo entre outros

---
`<header>`

cabeçalho da página. Pode conter logo, menus de avegação, aréa do usuário, barra de pesquisa, etc

---
`<main>`

conteudo principal da página, tudo o conteúdo que é contido por essa tag deve ser unico em toda a página. Não deve haver mais de um <main> por página e deve ser filho apenas de <body>

---
`<mark>`

ressalta uma parte do texto assim como um marcador de texto faz em uma folha de papel

---

`<nav>`

implementa uma serie de links de navegaçao do site, nao necessariamente todos os links do site.

---

`<section>`

é uma seçao dentro da página que esta sendo exibida

---

`<summary>`

é utilizado dentro de `<details>` como titulo para o elemento final

---

`<time>`

é usado para traduzir a hora para um formato legível pora a máquina, permitindo que os navegadores ofereçam lembretes de data por meio do calendário do usuário e que os mecanismos de busca produzam resultados de pesquisa mais inteligentes.

