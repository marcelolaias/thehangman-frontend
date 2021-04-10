<template>
    <div class="game-keyboard">
        <button 
            :disable="checkLetter(letter)"
            :key="key"
            v-for="(letter, key) in 'ABCDEFGHIJKLMNOPQRSTUVXWYZ0123456789'"
            v-on:click="pressKeyboardKey(letter)">
            {{letter}}
        </button>
    </div>
</template>

<script>

export default ({
    name: 'Keyboard',
    props: {
        checkLetter: Function,
        submittedLetters: Array,
        pressKeyboardKey: Function
    },
    data() {
        return {
            
        }
    },
    components: {

    },
    methods: {

    }
})
</script>

<style>
.game-keyboard {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  margin-top: 15px;
  width: 100%;    
}
.game-keyboard button {
  margin: 5px;
  width: 45px;
  text-transform: uppercase;
}
</style>