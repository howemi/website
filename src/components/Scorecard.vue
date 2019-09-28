<template>
  <div>
    <h1>Scorecard</h1>
    <b-container class="px-0">
      <table class="table">
        <thead class="thead-dark">
          <tr>
            <th scope="col" class="header header-top">#</th>
            <th v-for="(player, index) in players" :key="index" class="header header-top" scope="col">
              <Bro @add_name="add_player()" :index="index" class="header header-top" @remove_index="remove_player(index)"></Bro>
            </th>
            <th scope="col" @click="add_player" class="header header-top">Add Player</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(round, row_index) in rounds" :key="row_index">
            <th scope="row" class="header header-left">{{ row_index + 1 }}</th>
            <td v-for="(player, player_index) in players" :key="player_index">
              <form @submit.prevent="focus_next(player_index, row_index)">
                <input
                  type="number"
                  class="text-center form-control score"
                  v-model="scores[player_index][row_index]"
                />
              </form>
            </td>
          </tr>
          <tr v-if="players.length && rounds.length">
            <th class="header header-bottom header-left">Total</th>
            <td v-for="(player, player_index) in players" class="header header-bottom" :key="player_index">
              <span>{{ total(player_index) }}</span>
            </td>
          </tr>
          <tr>
            <th @click="add_round" scope="row" class="header header-left">Add round +</th>
          </tr>
        </tbody>
      </table>
    </b-container>
  </div>
</template>

<script>
// @ is an alias to /src
import Bro from "@/components/Bro.vue";
export default {
  components: {
    Bro
  },
  data() {
    return {
      edit: false,
      players: this.$store.state.players,
      rounds: this.$store.state.rounds,
      scores: this.$store.state.scores
    };
  },
  computed: {
    inputs: function() {
      return document.getElementsByClassName('score')
    }
  },
  methods: {
    add_player() {
      this.$store.state.scores.push([]);
      this.$store.state.players.push(this.$store.state.players.length + 1);
    },
    remove_player(index) {
      this.$store.state.players.splice(index, 1);
      this.$store.state.scores.splice(index, 1);
    },
    add_round() {
      this.rounds.push(this.rounds.length + 1);
    },
    total(index) {
      let total = 0;
      this.$store.state.scores[index].forEach(item => {
        total += parseInt(item);
      });
      return total;
    },
    focus_next($event, col, row) {
      console.log(col);
      console.log(row);
    }
  }
};
</script>

<style>
input[type="number"]::-webkit-outer-spin-button,
input[type="number"]::-webkit-inner-spin-button {
  -webkit-appearance: none;
  margin: 0;
}

.header {
  position: sticky;
  position: -webkit-sticky;
}
.header-top {
  top: -1px;
  z-index: 20;
}
.header-bottom {
  bottom: 0px;
  background: white
}
.header-left {
  left: 0px;
  background: lightgray;
  z-index: 10;
}

.container {
  overflow-x: auto;
  max-height: 500px;
}

input[type="number"] {
  -moz-appearance: textfield;
}
</style>