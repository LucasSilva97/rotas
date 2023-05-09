# Rotas

This project was generated with [Angular CLI](https://github.com/angular/angular-cli) version 15.2.6.

## Anatomia de Rotas

Afinal de contas, o arquivo Route também é um arquivo de Module, só que é utilizado para as rotas.
Dentro do app-routing.module, temos a importação do NgModule, para indicar que é um Módulo, a importação do RouteModule, e da classe Routes.
Abaixo teremos uma const route, do tipo route, onde teremos um array para criar objetos de rotas. 
Dentro do NgModule nós temos a importação RouteModule, e apontar para a raiz (forRoot) justamente o routes, ou seja, o array de objetos de rotas. 
Também é possível fazer a exportação do RouteModule, para utilizar em outros módulos, e também a exportação da classe do componente app-routing.module. 
Dessa forma, também, dentro do app.module podemos importar outros arquivos de rota que sejam criados.

## Criando as primeiras rotas

Criando um objeto de rotas, nós temos que passar algumas propriedades para rotear o componente que vai estar nesse objeto. 
- path: é o caminho da rota (pode ser padrão ou personalizada)
- component: qual é o componente que vai estar acessando
- pathMatch: prefix > caso o prefixo, no path, estiver vazio a url pode ter outras coisas além da url original, ou full > tem que exatamente igual ao que esteja sendo colocado no objeto, para indicar uma url exata. 


## Rotas coringas

Uma rota coringa é quando um usuário acesse qualquer rota que não seja mapeável, ele pode escolher o que fazer com ele.


## RouterLink

Quando queremos fazer um link a alguma outra página, outro conteúdo, geralmente utilizamos a tag <a></a> juntamente com seu atributo href="", porém, o problema disso é que sempre causa um refresh na página e no runing do Angular, o que é totalmente contrário ao conceito de sites que utilizando SPA. Então, para acessar essas rotas, utilizamos o routelink no lugar do href="", ficando dessa forma: [routerLink]="['']", dentro das aspas simples passamos o caminho que deve ser acessado. 

## ActiveRouter

[routerLinkActive]="['classe']" > nos permite associar uma classe CSS ao link ativo, pois o routerLinkActive está dando um comportamento de classe para o link.

Ainda podemos utilizar o [routerLinkActiveOptions]="{exact: true}", para garantir que todos as tags <a> com routerlink só tenha aquelas propriedades da classe CSS se o link estiver ativo/selecionado.

## Recuperando Parametros das Rotas

Inicialmente, dentro do app-routing.module, devemos alterar o path do componente que queremos acessar e colocar um parâmetro a mais, como por exemplo um id = 'exemplo/:id'. 
Dentro da parte lógica do componente, fazemos uma injeção de dependências, onde o constructor vai ter como parâmetro uma propriedade private da class ActivatedRoute. Através dessa propriedade conseguimos acessar seus parâmetros, e dentro desses parâmetros, temos o subscribe. E por sua vez, o subscribe consegue acessar o value dessa propriedade, onde vai conter seu id.

## Recuperando QueryParams de Rotas

// http://localhost:4200/portifolio/1?name=lucas&token=123

Imaginando um usuário que digite alguns dados, onde você vai submeter esses dados à uma API, ou nesse caso passar para um QueryParams da URL. A forma correta de tratar é acessando os queryParams, e através do subscribe conseguimos acessar/recuperar os dados passados no queryParams. Essa é a diferença em relação ao params somente passando, onde o mesmo recupera o id. 

## Redirecionamento por componente

Para utilizar, devemos injetar outra dependência do tipo :Router, que vem do @angular/router, que será importado.
Dentro do ngOnInit, podemos acessar através da propriedade do tipo Router o navigate(), que permite passar uma rota específica para a qual queremos navegar.

## Rotas children

Uma das propriedades dentro de um objeto do array do route, é o children. Então dentro dele, podemos passar outro objeto que vai ser uma "rota filha" do objeto pai que vai estar recebendo essa rota. Por exemplo:

{path:'/exemplo', component: ExemploComponent, children:[
  {path:':id', componentGeneric},
  {path:':id', componentFilho},
  {path:':id', componentFilho},
]}
 então podemos acessar, nesse caso:

 - url/exemplo
 e também suas rotas filhas:

- url/exemplo/1 ou 2 ou 3, etc...

## Parâmetros de rotas children

Para acessar os parâmetros de uma rota filha, podemos acessar através do children, ou firstChild, que são propriedades da class ActivatedRoute do Angular. 
