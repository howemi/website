<template>
  <div @mouseup="$refs.input_field.focus()">
    <input
      v-if="edit"
      v-model="player_name"
      @blur="change_name"
      @keyup.enter="change_name"
      
      ref="input_field"
      type="text"
      class="form-control"
    />
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
    this.$refs.input_field.focus();
  },
};
</script>

<style scoped>
input {
  width: 100px;
  margin: auto;
}
</style>