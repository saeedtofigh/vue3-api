<template>
  <Header />
  <router-view class=" my-5 text-center" />
</template>
<script>
  import Header from '@/components/Header.vue';

  export default {
    name: 'App',
    components: { Header },
  };
</script>
<style>
  #app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    color: #2c3e50;
  }

  #nav a {
    font-weight: bold;
    color: #222;
    font-size: 1.4rem;
    text-decoration: none;
  }

  #nav a.router-link-exact-active {
    color: #42b983;
  }
</style>
