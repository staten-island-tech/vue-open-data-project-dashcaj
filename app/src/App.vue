<script setup>
import { RouterLink, RouterView } from 'vue-router'
import HelloWorld from './components/HelloWorld.vue'

const api = "https://data.cityofnewyork.us/resource/43nn-pn8j.json"
async function fetchData(api) {
  try {
    const response = await fetch(api);
    const data = await response.json();
    

    console.log(data);
  }
  catch (error) {
    console.log(error);
  }
}
fetchData(api);
</script>

<template>
  <header>


    <div class="wrapper">


      <nav>
        <RouterLink to="/">home       </RouterLink>
        <RouterLink to="/brooklyn">brooklyn      </RouterLink>
        <RouterLink to="/queens">queens     </RouterLink>
        <RouterLink to="/bronx">bronx     </RouterLink>
        <RouterLink to="/manhattan">manhattan     </RouterLink>
        <RouterLink to="/statenisland">staten island     </RouterLink>
      </nav>

      <div ></div>
      
    </div>
  </header>

  <RouterView />
</template>

<style scoped>

</style>
