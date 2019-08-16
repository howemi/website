<template>
  <transition>
  <b-navbar ref="nav" toggleable="lg" type="dark" variant="danger" :sticky="true" v-scroll="mesid">
    <b-spinner small type="grow" class="mr-4 text-warning"></b-spinner>
    <b-navbar-brand class="mr-0">
      <router-link to="/">D E S I G N</router-link>
    </b-navbar-brand>

    <b-navbar-toggle target="nav-collapse"></b-navbar-toggle>

    <b-collapse id="nav-collapse" is-nav>
      <div class="mx-2"></div>
      <b-navbar-nav>
        <b-nav-item>
          <router-link to="/">Home</router-link>
        </b-nav-item>
        <b-nav-item>
          <router-link to="/about">About</router-link>
        </b-nav-item>
        <b-nav-item>
          <router-link to="/scorecard">Scorecard</router-link>
        </b-nav-item>
        <b-nav-item>
          <router-link to="/credits">ALL THE CREDIT</router-link>
        </b-nav-item>
      </b-navbar-nav>

      <!-- Right aligned nav items -->
      <b-navbar-nav class="ml-auto">
        <b-nav-form class="justify-content-center">
          <b-form-input size="sm" class="mr-sm-2" placeholder="Search"></b-form-input>
          <b-button size="sm" class="my-2 my-sm-0" type="submit">Search</b-button>
        </b-nav-form>

        <b-nav-item-dropdown text="Region" right>
          <b-dropdown-item
            v-for="lang in languages"
            :key="lang"
            @click="change_lang(lang)"
          >{{ lang }}</b-dropdown-item>
        </b-nav-item-dropdown>
      </b-navbar-nav>
    </b-collapse>
  </b-navbar>
  </transition>
</template>

<script>
export default {
  data: function() {
    return {
      languages: ["EN", "DK", "ES"],
      current_scroll: 0
    };
  },
  methods: {
    change_lang(lang) {
      this.$store.commit("mutateStateField", { language: lang });
    },
    mesid() {
      let diff =  window.scrollY - this.current_scroll;

      if (diff > 0) {
        // Scrolling Down
        this.$refs.nav.style.top = '-60px'
      } else {
        // Scrolling Up
        this.$refs.nav.style.top = '0px'
      }
      this.current_scroll = window.scrollY;
    }
  }
};
</script>

<style>
nav a {
  color: #fff;
}
ul.dropdown-menu {
  max-height: 200px;
  overflow: auto;
}
li a.router-link-exact-active {
  color: #333;
}
</style>