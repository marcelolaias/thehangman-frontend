<template>
  <div class="grid-container">
    <div class="grid-item" id="monitor">
        <img class="clock-img" 
             :src="require(`../assets/clock.svg`)" />
        {{ this.countDown }}
    </div>
    <div class="grid-item">
      <div class="game-body">
        <EndGame :step="step" v-if="step === 'LOSER' || step === 'WINNER'" />
        <Gallows :errors="errors" />
        <Word :word="word" :tip="tip" :checkLetter="checkLetter" :step="step" />
        <div class="keyboard">
          <Keyboard
            v-if="step === 'game'"
            :submittedLetters="submittedLetters"
            :checkLetter="checkLetter"
            :pressKeyboardKey="pressKeyboardKey"
          />
        </div>
        <button class="button-save" v-on:click="saveGame">Save Game</button>
      </div>
    </div>
    <div class="grid-item">
        <img class="new-word-img" 
             v-on:click="newGame"
             :src="require(`../assets/newWord.svg`)" />
        New word
    </div>
  </div>
</template>

<script>
import Gallows from "./Gallows";
import Word from "./Word";
import Keyboard from "./Keyboard";
import EndGame from "./EndGame";

export default {
  name: "GameBody",
  props: {
    word: String,
    tip: String,
    errors: Number,
    step: String,
    countDown: Number,
    submittedLetters: Array,
    checkLetter: Function,
    pressKeyboardKey: Function,
    newGame: Function,
    saveGame: Function
  },
  data() {
    return {};
  },
  components: {
    Gallows,
    Word,
    Keyboard,
    EndGame,
  },
  methods: {},
};
</script>