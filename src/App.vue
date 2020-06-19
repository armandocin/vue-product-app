<template>
  <div id="app">
    <NavBar msg="Welcome to Your Vue.js App"/>
    <Product />
  </div>
</template>

<script>
import NavBar from './components/Navbar.vue'
import Product from './components/Product.vue'

export default {
  name: 'App',
  components: {
    NavBar,
    Product
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}

h3 {
  margin: 40px 0 0;
}
a {
  color: #42b983;
  cursor: pointer;
}
</style>
