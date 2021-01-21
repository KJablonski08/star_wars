<template>
  <div id="app">
    <AppNavigation @inputData="updateMode" />
    <FilmCards :mode="mode" />
  </div>
</template>

<script>
import AppNavigation from './components/AppNavigation.vue'
import FilmCards from './components/FilmCards.vue'

export default {
  name: 'App',
  components: {
    AppNavigation,
    FilmCards,
  },
  data: function() {
		return {
			mode: null,
      results: null,
		};
	},
  methods: {
		updateMode(variable) {
			this.mode = variable;
		},
	},
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
}
</style>
