<template>
  <div class="last-moves-list">
    <table>
      <thead>
        <th>Date</th>
        <th>Errors</th>
        <th>Finished</th>
        <th>Actions</th>
      </thead>
      <tbody>
        <tr :key="key" v-for="(row, key) in records">
          <td>{{row.date}}</td>
          <td>{{row.errors}}</td>
          <td><input type="checkbox" :checked="row.finished" ></td>
          <td>
              <img class="play-img" :src="require(`../assets/play.png`)" 
                   v-if="!row.finished"
                   v-on:click="showGame(row)" />
          </td>
        </tr>
      </tbody>
    </table>
    <button class="button1" v-on:click="newGameAction">
      New Game
    </button>
  </div>
</template>

<script>


export default {
  name: "LastMovesList",
  props: {
    records: Array,
    newGameAction: Function,
    showGame: Function
  },
  data() {
    return {

    }    
  },
  components: {},
  computed: { },  
  methods: { },
};
</script>
<style>
.last-moves-list {
    display: flex;
    flex-direction: column;
    align-content: center;
}
.last-moves-list button {
    margin-top: 20px;
}
.play-img {
    cursor: pointer;
    height: 25px;
}
</style>