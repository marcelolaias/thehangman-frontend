<template>
    <div class="game-word">
        <div class="word-letters">
            <div class="word-letter"
                 :key="key"
                 v-for="(letter, key) in word">
                 {{ checkLetter(letter) || step === 'hanged' ? letter : '' }}
            </div>
        </div>

        <div class="word-tip">{{tip}}</div>
    </div>
</template>

<script>

export default ({
    name: 'Word',
    props: {
        word: String,
        tip: String,
        checkLetter: Function,
        step: String
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
.game-word {
    display: flex;
    flex-direction: column;
    text-align: center;
    text-transform: uppercase;
    align-items: center;
}

.word-letters {
    display: flex;
    margin-bottom: 20px;
}

.word-letter {
    display: flex;
    height: 30px;
    width: 30px;
    margin: 0 5px;
    border-bottom: 1px solid var(--color-text-light);
    justify-content: center;
    align-items: center;
}
</style>