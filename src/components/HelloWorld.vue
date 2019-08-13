<template>
  <div class="hello">
    <div v-if="$store.state.language === 'DK'">
      <img class="flag" src="https://cdn.rawgit.com/hjnilsson/country-flags/master/svg/dk.svg">
      <h1>Hej</h1>
    </div>
    <div v-else-if="$store.state.language === 'EN'">
      <img class="flag" src="https://cdn.rawgit.com/hjnilsson/country-flags/master/svg/us.svg">
      <h1>Hello</h1>
    </div>
    
    <p>Your selected language is: {{language}}</p>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },
  computed: {
    language: function() {
      if(this.$store.state.language == 'EN') {
        return 'English'
      } else if (this.$store.state.language == 'DK') {
        return 'Danish'
      }
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.flag {
  height: 20px;
}
h3 {
  margin: 40px 0 0;
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
