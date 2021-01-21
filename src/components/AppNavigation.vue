<template>
  <div>
    <b-navbar toggleable="lg" type="dark" variant="dark">
      <b-navbar-brand><img alt="Vue logo" src="../assets/logo.png"></b-navbar-brand>

      <b-navbar-toggle target="nav-collapse"></b-navbar-toggle>

      
    </b-navbar>
  </div>
</template>

<script>
export default {
  name: 'AppNavigation',
  props: {
    msg: String
  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  img {
    height: 3em;
  }
</style>
