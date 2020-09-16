<template>
  <div class="hello">
    <div v-if="$store.state.language === 'DK'">
      <img class="flag my-3" src=".${publicPath}/assets/flags/DK.svg">
      <h1>Hej</h1>
    </div>
    <div v-else-if="$store.state.language === 'EN'">
      <img class="flag my-3" src=".${publicPath}/assets/flags/EN.svg">
      <h1>Hello</h1>
    </div>
    <div v-else-if="$store.state.language === 'ES'">
      <img class="flag my-3" :src="${publicPath}/assets/flags/ES.svg">
      <h1>Hola</h1>
    </div>

    <p id="test">Your selected language is: {{language}}</p>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },
  data() {
    return {
      publicPath: "./scorecard/"
    }
  },
  computed: {
    language: function() {
      if (this.$store.state.language == 'DK') {
        return 'Danish'
      } else if (this.$store.state.language == 'ES') {
        return 'Spanish'
      } else {
        return 'English'
      }
    },
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.flag {
  height: 60px;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
