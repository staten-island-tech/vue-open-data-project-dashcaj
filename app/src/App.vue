<script setup>
import { RouterLink, RouterView } from 'vue-router'
import HelloWorld from './components/HelloWorld.vue'

const api = "https://data.cityofnewyork.us/resource/hjae-yuav.json"
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
        <RouterLink to="/open">open parks      </RouterLink>
        <RouterLink to="/handicap">open vs. accessible    </RouterLink>
        <RouterLink to="/cards">all handicap accessible    </RouterLink>
      </nav>

      <div ></div>
      
    </div>
  </header>

  <RouterView />
</template>

<style scoped>

</style>
