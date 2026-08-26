# Formulários
### O que são 

Em HTML os fomulários são usados para capturar a entrada de dados do usuário através dos inputs. É representado pela tag `<form>` e assim como `<section>`, é um container que abraça diversos outros componentes conhecidos como **Form Elements**, esses elementos são responsaveis pela captura de dados e cada um tem sua função.

### Uso do form

Como dito anteriormente o form funciona como um container, então podemos usa-lo da seguinte forma:

````HTML
<form>
.
form elements
.
</form>
````

Este é o principio basico de um formulário, se você colocar um input do lado de fora o mesmo não participará da submissão daquele <form>. Agora, suponhamos que queira um formulario para cadastro de usuário, podemos implementa-lo assim:

````HTML
    <form onsubmit="onSubmit(event)">
        <label for="username-input">Nome de Usuário</label>
        <input id="username-input" type="text" name="username" />
        <br>
        <label for="email-input">Email</label>
        <input id="email-input" type="email" name="email" />
        <br>
        <label for="password-input">Senha</label>
        <input id="password-input" type="password" name="password" />
        <br>
        <input type="submit" value="Enviar">
    </form>
````

O que pode se observar nesse exemplo é o atributo de evento HTML **`onsubmit`** do form, esse parametro é utilizado junto ao input de submit no fim do formulário, ao clicar no input o evento de submissão é disparado e chama a função especificada no parametro, nesse caso ***"onSubmit()"***, passando o "event da submissão" do formulário. O event é o objeto SubmitEvent, que contém informações relacionadas àquele evento.

> *você pode ver o código de onSubmit() no arquivo index.html*

Outra possibilidade é utilizar o ***action*** aliado ao ***method*** para fazer uma requisição http direto do form:

````HTML
    <form action="/users" method="post">
        ...
    </form>
````

O action pode ser utilizado com os metodos **GET** e **POST**. 

````javascript
POST = simplesmente coloca os dados no corpo da requisição.  
GET  = normalmente os coloca na URL.
````

> <span style="color: red;">Importante</span> :  Nem Post nem Get garantem a segurança das requisições.

Vale destacar que em ambos os casos o parametro `name` dos inputs é passado como chave para o valor dos inputs no event. Esse parâmetro é extremamente importante para poder identificar os campos dentro do evento para que possam ser manipulados via Javascript.

#### Pegando o valor de username no javascript:
````javascript
function onSubmit(event) {
    event.preventDefault();

    const formData = new FormData(event.currentTarget);

    console.log(formData.get("username"));  //mostra o valor de username no console;
}
````

# Form Elements

Abaixo listo alguns elementos que podem ser utilizados junto ao form

`<input>` → Elemento usado para entrada de dados, oferecendo diferentes tipos de controle através do atributo type, como texto, senha, email, número, checkbox e radio.

`<label>` → Define o texto descritivo de um campo e permite associá-lo a um elemento de formulário, melhorando usabilidade e acessibilidade.

`<select>` → Cria uma lista de opções na qual o usuário pode selecionar um ou mais valores.

`<textarea>` → Cria um campo de texto destinado à entrada de conteúdos maiores e que podem ocupar múltiplas linhas.

`<button>` → Cria um botão que pode executar ações, como enviar um formulário, redefini-lo ou executar código JavaScript.

`<fieldset>` → Agrupa elementos relacionados de um formulário, permitindo organizar semanticamente um conjunto de campos.

`<legend>` → Define o título ou descrição de um `<fieldset>`, identificando o grupo de campos que ele contém.

`<datalist>` → Fornece uma lista de sugestões pré-definidas que podem ser exibidas enquanto o usuário preenche um `<input>`.

`<output>` → Representa o resultado de um cálculo ou de uma ação realizada pelo usuário ou pelo formulário.

`<option>` → Define uma opção que pode ser selecionada dentro de elementos como `<select>` e `<datalist>`.

`<optgroup>` → Agrupa opções relacionadas dentro de um `<select>`, permitindo organizar listas grandes de opções.
