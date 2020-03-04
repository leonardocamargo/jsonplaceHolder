# project JsonPlaceHolder
Projeto de automação de testes da api   **https://jsonplaceholder.typicode.com/**

## Versão
A versão atual é a 1.0.0, sujeita a alteração devido as modificações.


### Rodando no Postman IDE
- Importe o arquivo **json_placeholdertest.json** no Postman e rode a Collection ou apenas cenarios especificos.


### Newman Instalação em ambiente Linux sem Docker

- Newman builda com o Node.js. Para rodar o  Newman, você precisa ter o  Node.js instalado.
- Node.js Latest Version [Node.js](https://nodejs.org/en/)

- Após ter o Node.js instalado execute o seguinte comando: 
```
$ npm install -g newman```




Com o newman instalado, para rodar é simples:
```
$ newman run "MY_COLLECTION"```
No caso, seria:

```
$ newman run json_placeholdertest.json```


### Newman Instalação em ambiente linux com Docker

Documentação: https://hub.docker.com/r/postman/newman/


Basicamente:

- Dar o pull da imagem do newman        ```docker pull postman/newman```
- Buildar a imagem                      ```docker build -t postman/newman:alpine --build-arg NEWMAN_VERSION="full semver version" docker/images/alpine```          (Buildando a imagem do newman com o Alpine, passando a ultima versão do newman como argumento)
- Depois, rodar o comando run para rodar os testes ```docker run -v ~/collections:/etc/newman -t postman/newman:alpine json_placeholdertest.json```     (Está rodando a imagem criando um volume dentro do container, onde vc precisa passar onde está o seu arquivo localmente na sua máquina e depois passar o /etc/newman, pois o container do newman, por default, procura o arquivo na pasta simbolica criada "etc/newman")



### Observações: 

- Adicionei alguns comentarios nos testes que executei, pois testei o comportamento que deveria ter e não o que ela está refletindo atualmente.
- Não consegui parametrizar o iD do Post em algumas chamadas GET, pois o "parseInt" não funcionou no Newman.
-Por ser uma api que já está em produção e estamos validando dados "reais", não é plausivel validar o conteudo do title, do body, por ser uma api publica e em funcionamento, pode sofrer varias alterações, como exclusão de publicações, alterações de titulos e adição de comentarios nas publicações da Api.
-Criei um teste que faz a validação da existencia de um post, apenas para fim de ter uma validação. Mas acredito que o melhor cenario seria fazer um e2e ou mockar os dados antes de fazer a chamada. (isso em ambiente de testes)
- O mesmo serve para o /posts na criação de um post. Por ser algo público e que não está no dominio, nao é possivel validar o Id que foi criado de uma publicação. 
- Validação de usuario inexistente no post é difícil mensurar pois não temos acesso a base de dados, as vezes passando um usuario extenso "129122191298", pode ter na base de dados.


