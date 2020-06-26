<template>
  <nav class="nav-bar">
    <a :href="vueHome" target="_blank">
      <img alt="Vue logo" src="../assets/logo.png" height="50px" width="50px">
    </a>
    <router-link to="/">Home</router-link>
    <router-link to="/about">About</router-link>
  </nav>
</template>

<script>
export default {
  name: 'NavBar',
  props: {
    msg: String
  },
  data: () => ({
    vueHome: 'https://vuejs.org/'
  })
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  ul {
    list-style-type: none;
    padding: 0;
  }
  li {
    display: inline-block;
    margin: 0 10px;
  }
  .nav-bar {
    background: linear-gradient(-90deg, #84CF6A, #16C0B0);
    height: 60px;
    margin-bottom: 15px;
    color: #000;
  }

  .nav-bar a {
    color: #000;
    margin-right: 24px;
  }

  .nav-bar a:hover {
    color: #444;
  }
</style>
