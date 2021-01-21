<template>
  <div id="app">
    <AppNavigation @inputData="updateEndPoint"/>
  </div>
</template>

<script>
import AppNavigation from './components/AppNavigation.vue'

export default {
  name: 'App',
  components: {
    AppNavigation
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
