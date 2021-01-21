<template>
  <div>
    <b-navbar toggleable="lg" type="dark" variant="dark">
      <b-navbar-brand><img alt="Vue logo" src="../assets/logo.png"></b-navbar-brand>

      <b-navbar-toggle target="nav-collapse"></b-navbar-toggle>

      <b-collapse id="nav-collapse" is-nav>
        <!-- Right aligned nav items -->
        <b-navbar-nav class="ml-auto">
          <b-nav-item-dropdown text="Resource" right>
            <b-dropdown-item>Films</b-dropdown-item>
            <b-dropdown-item>Planets</b-dropdown-item>
            <b-dropdown-item>Spaceships</b-dropdown-item>
            <b-dropdown-item>Vehicles</b-dropdown-item>
            <b-dropdown-item>People</b-dropdown-item>
            <b-dropdown-item>Species</b-dropdown-item>
          </b-nav-item-dropdown>
        </b-navbar-nav>
      </b-collapse>
    </b-navbar>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  props: {
    msg: String
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  img {
    height: 3em;
  }
</style>
