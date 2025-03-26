<template>
<h1>amount of parks open in each borough</h1>
<div class="bar">
    <Bar :data="chartData" :options="chartOptions" />
</div>

</template>

<script>
import { defineComponent, onMounted, ref } from 'vue';
import { Bar } from 'vue-chartjs';
import { Chart as ChartJS, BarController, BarElement, CategoryScale, LinearScale } from 'chart.js';

ChartJS.register(BarController, BarElement, CategoryScale, LinearScale);

export default defineComponent({
  components: {
    Bar
  },
  setup() {
    const chartData = ref({
      labels: [],
      datasets: []
    });
    const chartOptions = ref({
      responsive: true,
      scales: {
        y: {
          beginAtZero: true
        }
      }
    });
    const apiUrl = 'https://data.cityofnewyork.us/resource/hjae-yuav.json';

    onMounted(async () => {
      try {
        const response = await fetch(apiUrl);
        const data = await response.json();
        

        const filteredData = data.filter(item => item.open_year_round === 'Yes' && item.borough);

        const boroughCounts = {};
        filteredData.forEach(item => {
          boroughCounts[item.borough] = (boroughCounts[item.borough] || 0) + 1;
        });


        chartData.value = {
          labels: Object.keys(boroughCounts),
          datasets: [{
            label: '#',
            data: Object.values(boroughCounts),
            backgroundColor: ['#3e53ab', '#ab743e', '#806b2f', '#381b82', '#9C27B0'],
          }]
        };
      } catch (error) {
        console.error('Error fetching data:', error);
      }
    });

    return {
      chartData,
      chartOptions
    };
  },
  template: '<Bar :data="chartData" :options="chartOptions" />'
});
</script>

<style>
.bar{
    width: 80%;
    height: 80%;
    text-align: center;
}
</style>


