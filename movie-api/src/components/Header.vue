<template>
<div class="header bg-white text-black p-3 shadow d-flex flex-row align-items-center" id="nav">
  <h2 class="mx-3">Movie</h2>
    <router-link class="mx-3" to="/">Home</router-link> 
    <router-link class="mx-3" to="/about">About</router-link> 
    <router-link class="mx-3" to="/article">Movies</router-link>
  </div>
        
    
</template>
<script>
export default {
    name: 'Header'
}
</script>