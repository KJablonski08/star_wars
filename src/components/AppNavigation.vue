<template>
  <div>
    <b-navbar toggleable="lg" type="dark" variant="dark" v-if="!checked">
      <b-navbar-brand><img alt="Vue logo" src="../assets/logo.png"></b-navbar-brand>
      <b-form-checkbox v-model="checked" name="check-button" switch class="ml-auto dark" v-on:change="submit">The Dark Side
      </b-form-checkbox>
    </b-navbar>
    <b-navbar toggleable="lg" type="dark" variant="light" v-if="checked">
      <b-navbar-brand><img alt="Vue logo" src="../assets/logo.png"></b-navbar-brand>
      <b-form-checkbox v-model="checked" name="check-button" switch class="ml-auto" v-on:change="submit">
      The Force
      </b-form-checkbox>
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
        checked: false
      }
    },
    methods: {
		submit: function() {
			this.$emit('inputData', this.checked)
		},
	},
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  img {
    height: 3em;
  }
  .dark {
    color: white;
  }

</style>
