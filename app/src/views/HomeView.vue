<script setup>
import TheWelcome from '../components/TheWelcome.vue'
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
  <main>
    <TheWelcome />
  </main>
</template>
