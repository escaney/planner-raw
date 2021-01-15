<template>
  <Nav />
  <router-view/>
</template>

<script>
  import Nav from "./components/Nav.vue"

  export default {
    components: { Nav }
  }
</script>

<style>
body {
  background-color: #fafafa;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  max-width: 600px;
  margin: 0 auto;
  color: #555;
}
</style>
