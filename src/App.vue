<template>
  <div id="app" :class="mode">
    <Navigation/>
    <div class="spacer"></div>
    <router-view class="test"/>
  </div>
</template>

<script>
import Navigation from '@/components/Navigation.vue'

export default {
  components: {
    Navigation
  },
  mounted: function() {
    let date = new Date()
    let time = date.getHours()
    if(time < 12) {
      document.title = "Good Morning!"
    } else if (time >= 12 && time < 18) {
      document.title = "Good Afternoon"
    } else  {
      document.title = "Good Evening"
    }
  },
  computed: {
    mode: function() {
      if(this.$store.state.mode == "dark") {
        return "dark"
      } else {
        return ""
      }
    }
  }

}
</script>

<style>
@import url('https://fonts.googleapis.com/css?family=Arvo|Montserrat&display=swap');
h1 {
  font-family: 'Arvo';
}


#app {
  font-family: 'Montserrat', 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  height: 100%;
  min-height: 100vh;
}

#app.dark {
  background-color: rgb(42, 42, 42);
  color:white;
}

.spacer {
  padding: 30px;
}

#nav a {
  font-weight: bold;
  color: #2c3e50;
}

#nav a.router-link-exact-active {
  color: #42b983;
}
</style>
