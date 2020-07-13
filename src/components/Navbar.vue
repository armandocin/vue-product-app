<template>
  <nav class="nav-bar">
    <div class="nav-content container-wide">
      <a :href="vueHome" target="_blank">
        <img alt="Vue logo" src="../assets/logo.png" height="50px" width="50px">
      </a>
      <router-link to="/">Home</router-link>
      <router-link to="/about">About</router-link>
    </div>
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
    background: #aacf6d;
    height: 60px;
    margin-bottom: 15px;
    color: #000;
  }

  .nav-bar a {
    color: #35495e;
    font-weight: bolder;
    margin-right: 24px;
    text-decoration: none;
    padding: 8px;
  }

  .nav-bar a:hover {
    color: #aacf6d;
    background-color: #35495e;
    border-radius: 4px;
  }

  .nav-content {
    height: 100%;
    display: flex;
    align-items: center;
  }
</style>
