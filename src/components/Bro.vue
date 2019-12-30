<template>
  <div @mouseup="$refs.input_field.select()">
    <form v-if="edit" @submit="change_name">
      <input
        @blur="change_name"
        v-model="player_name"
        ref="input_field"
        type="text"
        class="form-control"
      />
    </form>
    <span v-else @mousedown="edit=true">{{ player_name }}</span>
  </div>
</template>

<script>
export default {
  name: "Bro",
  props: {
    index: Number
  },
  data: function() {
    return {
      edit: true,
      player_name: "Player " + (this.index + 1)
    };
  },
  methods: {
    change_name() {
      let vm = this
      this.edit = false
      if(this.player_name.length === 0) {
        vm.$emit('remove_index', vm.index)
      }
    }
  },
  mounted: function() {
    this.$refs.input_field.select();
  },
};
</script>

<style scoped>
input {
  width: 100px;
  margin: auto;
}
</style>