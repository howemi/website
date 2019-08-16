<template>
  <div>
    <b-container>
      <h1>Scorecard</h1>
      <table class="table">
        <thead class="thead-dark" sticky>
          <tr>
            <th scope="col">#</th>
            <th v-for="(player, index) in players" :key="index" scope="col">
              <Bro @add_name="add_player()" :index="index" @remove_index="remove_player(index)"></Bro>
            </th>
            <th scope="col" @click="add_player">Add Player</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(round, row_index) in rounds" :key="row_index">
            <th scope="row">{{ row_index + 1 }}</th>
            <td v-for="(player, player_index) in players" :key="player_index">
              <input type="number" class="form-control" v-model="scores[player_index][row_index]" />
            </td>
          </tr>
          <tr v-if="players.length && rounds.length">
            <th >Total</th>
            <td v-for="(player, player_index) in players" :key="player_index">
              <span>{{ total(player_index) }}</span>
            </td>
          </tr>
          <tr>
            <th @click="add_round" scope="row">Add round +</th>
            
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
      players: [],
      rounds: [],
      scores: []
    };
  },
  methods: {
    add_player() {
      this.scores.push([]);
      this.players.push(this.players.length + 1);
    },
    remove_player(index) {
      this.players.splice(index, 1);
    },
    add_round() {
      this.rounds.push(this.rounds.length + 1);
    },
    total(index) {
      let total = 0
      this.scores[index].forEach(item => {
        console.log(item)
        total += parseInt(item)
      })
      return total
    }
  }
};
</script>

<style>
</style>