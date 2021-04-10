<h1>Jogo The Hangman</h1> 

> Status do Projeto: :heavy_check_mark: :warning: (concluido)

### Tópicos 

:small_blue_diamond: [Descrição do projeto](#descrição-do-projeto)

:small_blue_diamond: [Regras do Jogo](#regras-do-jogo)

:small_blue_diamond: [Linguagens e libs utilizadas](#linguagens-e-libs-utilizadas)

:small_blue_diamond: [Como rodar a aplicação](#como-rodar-a-aplicação-arrow_forward)

... 


## Descrição do projeto 

<p align="justify">
  Fontend do jogo da forca escrito em NodeJS com o framework Vue.
</p>

## Regras do Jogo

:heavy_check_mark: O jogo é individual.

:heavy_check_mark: Peça ao usuário que selecione uma letra do alfabeto.

:heavy_check_mark: Se a letra estiver contida na palavra, o usuário terá outra chance, adivinhando a letra. 

:heavy_check_mark: Para revelar uma carta clique na letra na área do alfabeto que fará com que a letra seja revelada se estiver contida na palavra.

:heavy_check_mark: Se a letra está contida ou não na palavra retirada do alfabeto.

:heavy_check_mark: Se a letra não estiver contida na palavra então uma parte do carrasco será adicionada.

:heavy_check_mark: O jogo continua até que a palavra é adivinhada e todas as letras são reveladas e exibida a mensagem 'WINNER' ou todas as partes do carrasco são 
exibidas 'LOSER'.

:heavy_check_mark: O usuário tem 100 segundos para escolher uma letra e o cronômetro é reiniciado a cada escolha. Caso esgote o tempo o jogo termina.

:heavy_check_mark: Após 6 tentativas inválidas o jogo termina.



## Linguagens e libs utilizadas :books:

- [NodeJS](https://nodejs.org/pt-br/): versão 14.16.0
- [VueJS](https://vuejs.org/): versão 2.6.11
- [GraphQL](https://graphql.org/): versão 14.2.1
- [Apollo GraphQL](https://www.apollographql.com/): versão 14.2.1



## Como rodar a aplicação :arrow_forward:

No terminal clone o projeto do backend em um diretório, em seguida instale os módulos e execute: 

```
mkdir thehangman-backend
cd thehangman-backend
git clone https://github.com/marcelolaias/thehangman-backend.git
npm i
npm start
```

O backend do jogo em GraphQL estará disponível no seguinte endereço:
> http://localhost:4000/

Para mais informações sobre o backend, acesso o link:
> https://github.com/marcelolaias/thehangmen-backend

Em outro terminal clone o projeto do frontend em um diretório, em seguida instale os módulos e execute: 

```
mkdir thehangman-frontend
cd thehangman-frontend
git clone https://github.com/marcelolaias/thehangman-frontend.git
npm i
npm run serve
```

O frontend do jogo pode ser acessado pelo seguinte link:
>http://localhost:8080/

**Dica: Para desligar as variáveis de ambiente durante o jogo, mude a variável 'debug' para false no arquivo:linha '..\thehangmen-frontend\src\App.vue:69'**


## Linguagens, dependencias e libs utilizadas :books:

- [NodeJS](https://nodejs.org/pt-br/): versão 14.16.0
- [VueJS](https://vuejs.org/): versão 2.6.11
- [GraphQL](https://graphql.org/): versão 14.2.1
- [Apollo GraphQL](https://www.apollographql.com/): versão 14.2.1


## Licença 

The [MIT License]() (MIT)

Copyright :copyright: 2021 - The Hangman