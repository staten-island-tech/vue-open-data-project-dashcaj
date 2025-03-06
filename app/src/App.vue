<script setup>
import { RouterLink, RouterView } from 'vue-router'
import HelloWorld from './components/HelloWorld.vue'
</script>

<template>
  <header>


    <div class="wrapper">


      <nav>
        <RouterLink to="/">home       </RouterLink>
        <RouterLink to="/brooklyn">brooklyn      </RouterLink>
        <RouterLink to="/test">queens     </RouterLink>
        <RouterLink to="/test">bronx     </RouterLink>
        <RouterLink to="/test">manhattan     </RouterLink>
        <RouterLink to="/test">staten island     </RouterLink>
      </nav>
    </div>
  </header>

  <RouterView />
</template>

<style scoped>

</style>
