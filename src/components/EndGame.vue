<template>
  <div class="end-game">
    <div :class="`end-game-${step.toLowerCase()}`">
      {{ step }}
    </div>
  </div>
</template>

<script>
export default {
  name: "EndGame",
  props: {
    step: String,
  },
  data() {
    return {};
  },
  components: {},
  methods: {},
};
</script>

<style>
.end-game {
  display: flex;
  font-size: 20pt;
  font-weight: bold;
  padding-top: 15px;
}

.end-game-hanged {
  color: tomato;
}

.end-game-winner {
  color: green;
}
</style>