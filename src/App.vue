<template>
  <div id="app">
    <NavBar msg="Welcome to Your Vue.js App"/>
    <router-view/>
  </div>
</template>

<script>
  import NavBar from './components/Navbar.vue'

  export default {
    name: 'App',
    components: {NavBar}
  }
</script>

<style>
  #app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    color: #2c3e50;
  }

  body {
    font-family: tahoma, sans-serif;
    color:#282828;
    margin: 0px;
  }

  h3 {
    margin: 40px 0 0;
  }
  a {
    color: #42b983;
    cursor: pointer;
  }

  button {
    display: block;
    margin-top: 30px;
    border: none;
    background-color: #1E95EA;
    color: white;
    height: 40px;
    width: 100px;
    font-size: 14px;
    cursor: pointer;
    border-radius: 4px;
  }

  .container-wide {
    max-width: 1400px;
    margin-left: auto;
    margin-right: auto;
  }

  .button-disabled {
    background-color: #d8d8d8;
    cursor: default;
  }
</style>
