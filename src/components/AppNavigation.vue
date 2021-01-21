<template>
  <div>
    <b-navbar toggleable="lg" type="dark" variant="dark">
      <b-navbar-brand><img alt="Vue logo" src="../assets/logo.png"></b-navbar-brand>

      <b-navbar-toggle target="nav-collapse"></b-navbar-toggle>

      <b-collapse id="nav-collapse" is-nav>
        <!-- Right aligned nav items -->
        <b-navbar-nav class="ml-auto">
          <b-form-select v-model="selected" :options="options" size="sm" class="mt-3"></b-form-select>
          <div class="mt-3">Selected: <strong>{{ selected }}</strong></div>
        </b-navbar-nav>
      </b-collapse>
    </b-navbar>
  </div>
</template>

<script>
export default {
  name: 'AppNavigation',
  props: {
    msg: String
  },
  data() {
		return {
			selected: '',
       options: [
          { value: 'Films', text: 'Films' },
          { value: 'Planets', text: 'Planets' },
          { value: 'Spaceships', text: 'Spaceships' },
          { value: 'Vehicles', text: 'Vehicles' },
          { value: 'People', text: 'People'},
          {value: 'Species', text: 'Species'}
        ],
		};
	},
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  img {
    height: 3em;
  }
</style>
