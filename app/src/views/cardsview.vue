<template>
    <div class="container">
      <h2>all handicap accessible parks</h2>
    
      <div class="card-list">
        <div v-for="toilet in accessibleToilets" :key="toilet.name" class="card">
          <h2>{{ toilet.name }}</h2>
          <h3>Borough: {{ toilet.borough }}</h3>
        </div>
      </div>
    </div>
  </template>
  
  <script setup>
  import { ref, onMounted } from 'vue';
  
  const accessibleToilets = ref([]);
  

  const fetchToilets = async () => {
    try {
      let res = await fetch('https://data.cityofnewyork.us/resource/hjae-yuav.json');
      let data = await res.json();
      
  

      accessibleToilets.value = data.filter(toilet => toilet.handicap_accessible === 'Yes');
      
    } catch (error) {
      console.error("There is an error", error);
    }
  };

  onMounted(() => {
    fetchToilets();
  });
  </script>
  
  <style scoped>
  .container {
    padding: 20px;
  }
  
  h2 {
    text-align: center;
    margin-bottom: 20px;
  }
  
  .card-list {
    display: flex;
    flex-wrap: wrap;
    gap: 20px;
  }
  
  .card {
    background-color: #f9f9f9;
    border: 1px solid #ddd;
    border-radius: 8px;
    padding: 15px;
    width: 250px;
  }
  
  .card h2 {
    text-align: center;
    font-size: 18px;
  }
  
  .card h3 {
    font-size: 16px;
    color: #333;
  }
  </style>