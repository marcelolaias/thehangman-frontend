# The Hangman Frontend

Fontend do jogo da forca escrito em NodeJS com o framework Vue.

## Linguagens e libs utilizadas :books:

- [NodeJS](https://nodejs.org/pt-br/): versão 14.16.0
- [VueJS](https://vuejs.org/): versão 2.6.11
- [GraphQL](https://graphql.org/): versão 14.2.1
- [Apollo GraphQL](https://www.apollographql.com/): versão 14.2.1

## Instalação

No terminal, em uma diretório clone o projeto do backend, insta e execute: 

```
git clone https://github.com/marcelolaias/thehangman-backend
npm i
npm run serve
```

Em outro diretório clone o projeto do frontend: 

```
git clone https://github.com/marcelolaias/thehangman-frontend
npm i
npm run serve
```


# SCENES Regras do Jogo

A implementação das regras estão no projeto backend.

- O jogo é individual.
- Peça ao usuário que selecione uma letra do alfabeto.
- Se a letra estiver contida na palavra, o usuário terá outra chance, adivinhando a letra. 
- Para revelar uma carta clique na letra na área do alfabeto que fará com que a letra seja revelada se estiver contida na palavra.
- Se a letra está contida ou não na palavra retirada do alfabeto.
- Se a letra não estiver contida na palavra então uma parte do carrasco será adicionada.
- O jogo continua até que a palavra é adivinhada e todas as letras são reveladas e exibida a mensagem 'WINNER' ou todas as partes do carrasco são exibidas 'LOSER'.
- O usuário tem 100 segundos para escolher uma letra e o cronômetro é reiniciado a cada escolha. Caso esgote o tempo o jogo termina.
- Após 6 tentativas inválidas o jogo termina.
