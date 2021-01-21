<template>
  <div id="app">
    <AppNavigation @inputData="updateEndPoint"/>
    <FilmCards :endPoint="endPoint" />
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
			endPoint: null,
		};
	},
  methods: {
		updateEndPoint(variable) {
			this.endPoint = variable;
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
  color: #2c3e50;
}
</style>
