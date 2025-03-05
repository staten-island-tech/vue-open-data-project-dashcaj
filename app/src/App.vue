<script setup>
import { RouterLink, RouterView } from 'vue-router'
import HelloWorld from './components/HelloWorld.vue'
</script>

<template>
  <header>


    <div class="wrapper">


      <nav>
        <RouterLink to="/">home       </RouterLink>
        <RouterLink to="/about">charts      </RouterLink>
        <RouterLink to="/test">test     </RouterLink>
      </nav>
    </div>
  </header>

  <RouterView />
</template>

<style scoped>

</style>
