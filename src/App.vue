<template>
  <div id="gameBody">
    <div class="back-img" v-if="screen === 'game'">
      <img :src="require(`./assets/back.svg`)" v-on:click="gotoBackScreen" />
    </div>
    <h1>The Hangman Game</h1>
    
    <section id="debug" v-if="debug">
    Errors: {{ errors }}<br/> Step: {{ step }}<br/> Screen: {{ screen }}<br/>
    Word:{{ word }}<br/>Submitted Letters:{{ submittedLetters.join("") }}<br/>
    Exception: {{exception}}<br /> GraphQL: {{ graphqlCmd }}
    </section>

    <section id="lastMoves" v-if="screen === 'lastMoves'">
      <LastMovesList
        :records="lastMoves"
        :newGameAction="newGame"
        :showGame="showGame"
      />
    </section>

    <section id="game" v-if="screen === 'game'">
      <GameBody
        :word="word"
        :tip="tip"
        :errors="errors"
        :checkLetter="checkLetter"
        :step="step"
        :submittedLetters="submittedLetters"
        :pressKeyboardKey="pressKeyboardKey"
        :countDown="countDown"
        :newGame="newGame"
        :saveGame="saveGame"
      />
    </section>
  </div>
</template>

<script>
import "./theme/game.css";

import graphQl from "graphql-tag";
import LastMovesList from "./components/LastMovesList";
import GameBody from "./components/GameBody";

const graphqlGameStructure = `
{
  id
  date
  errors
  finished
  step 
  screen 
  submittedLetters 
  word {
    tip
    word
  }
}
`;

export default {
  name: "appTheHangman",

  data: function () {
    this.getLastMoves();

    return {
      debug: true,
      graphqlCmd: '',
      screen: "lastMoves",
      step: "lastMoves",
      exception: null,
      lastMoves: [],
      game: null,
      word: "",
      tip: "",
      interval: null,
      totalTime: 100000, //100 segundos
      errors: 0,
      countDown: 0,
      submittedLetters: [],
    };
  },

  components: {
    LastMovesList,
    GameBody,
  },

  methods: {
    getLastMoves() {
      this.$api
        .query({
          query: graphQl`{ lastMoves ${graphqlGameStructure} }`,
        })
        .then((resultSet) => {
          //this.records = resultSet.data.lastMoves
          this.lastMoves = resultSet.data.lastMoves;
          this.errors = null;
        })
        .catch((err) => {
          this.exception = err;
        });
    },
    newGame() {
      this.graphqlCmd = `mutation { newGame { id date errors finished step screen submittedLetters word { tip word } } }`
      this.$api
        .mutate({
          mutation: graphQl`${this.graphqlCmd}`,
        })
        .then((graphql) => {
          this.game = graphql.data.newGame;
          this.word = graphql.data.newGame.word.word;
          this.tip = graphql.data.newGame.word.tip;
          this.submittedLetters = graphql.data.newGame.submittedLetters.split("");
          this.errors = graphql.data.newGame.errors;
          this.screen = graphql.data.newGame.screen;
          this.step = graphql.data.newGame.step;
        })
        .catch((err) => {
          this.exception = err;
        });
    },
    saveGame: function (reload = true) {
      this.graphqlCmd = `mutation { 
                    saveGame(
                      id:${this.game.id}
                      word:"${this.word}"
                    ) 
                    ${graphqlGameStructure} 
                }`;
      this.$api
        .mutate({ mutation: graphQl`${this.graphqlCmd}` })
        .then((graphql) => {
          this.game = graphql.data.saveGame
          if (reload) location.reload();
        })
        .catch((err) => {
          this.exception = err;
        });
    },
    showGame: function (game) {
      this.game = game;
      this.word = game.word.word;
      this.tip = game.word.tip;
      this.submittedLetters = game.submittedLetters.split("");
      this.errors = game.errors;
      this.screen = game.screen;
      this.step = game.step;
    },
    checkLetter: function (letter) {
      return this.submittedLetters.find((l) => {
        return l.toLowerCase() === letter.toLowerCase();
      });
    },
    // checkErrors: function (letter) {
    //   let result = this.word.toLowerCase().indexOf(letter.toLowerCase());
    //   if (result >= 0) {
    //     return this.checkHits();
    //   }

    //   this.errors++;

    //   if (this.errors >= 6) {
    //     this.step = "LOSER";
    //     this.errors = 6;
    //     if (this.interval) window.clearInterval(this.interval);
    //   }
    // },
    // checkHits: function () {
    //   let uniqueLetters = [...new Set(this.word.split(""))];
    //   let value = this.submittedLetters.length - this.errors;
    //   if (uniqueLetters.length === value) {
    //     this.step = "WINNER";
    //     if (this.interval) window.clearInterval(this.interval);
    //   }
    // },
    pressKeyboardKey: function (letter) {
      this.graphqlCmd = `mutation { 
                    submitLetter(
                      id:${this.game.id}
                      word:"${this.word}"
                      letter:"${letter}"
                    ) 
                    ${graphqlGameStructure} 
                }`;
      this.$api
        .mutate({ mutation: graphQl`${this.graphqlCmd}` })
        .then((graphql) => {
          this.game = graphql.data.submitLetter;
          this.submittedLetters = this.game.submittedLetters.split("");
          this.errors = this.game.errors;
          this.screen = this.game.screen;
          this.step = this.game.step;
          this.startCountDown();
        })
        .catch((err) => {
          this.exception = err;
        });
    },
    startCountDown: function () {
      this.countDown = this.totalTime / 1000;
      if (this.interval) window.clearInterval(this.interval);
      if (this.step == "game")
        this.interval = window.setInterval(this.subtractCountDown, 1000);
    },
    subtractCountDown: function () {
      this.countDown--;
      if (this.countDown <= 0) {
        if (this.interval) window.clearInterval(this.interval);
        this.step = "LOSER";
        this.errors = 6;
      }
    },
    gotoBackScreen: function () {
      if (this.interval) window.clearInterval(this.interval);
      location.reload();
    },
  },
};
</script>

<style>
</style>