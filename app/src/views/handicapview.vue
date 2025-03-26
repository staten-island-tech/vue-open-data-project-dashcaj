<template>
        <h1>handicap accessible vs not</h1>

        <div class="donut">
                <Doughnut :data="chartData" :options="chartOptions" />
        </div>
        
</template>

<script>
import { defineComponent, onMounted, ref } from 'vue';
import { Doughnut } from 'vue-chartjs';
import { Chart as ChartJS, DoughnutController, ArcElement, CategoryScale, LinearScale, Tooltip } from 'chart.js';

ChartJS.register(DoughnutController, ArcElement, CategoryScale, LinearScale, Tooltip);

export default defineComponent({
  components: {
    Doughnut
  },
  setup() {
    const chartData = ref({
      labels: ['open all year', 'handicap'],
      datasets: []
    });
    const chartOptions = ref({
      responsive: true,
      plugins: {
        tooltip: {
          enabled: true,
          callbacks: {
            label: function (tooltipItem) {
              let dataset = tooltipItem.dataset;
              let value = dataset.data[tooltipItem.dataIndex];
              return `${dataset.label}: ${value}`;
            }
          }
        }
      }
    });
    const apiUrl = 'https://data.cityofnewyork.us/resource/hjae-yuav.json';

    onMounted(async () => {
      try {
        const response = await fetch(apiUrl);
        const data = await response.json();
        

        const openYearRoundCount = data.filter(item => item.open_year_round === 'Yes').length;
        const handicapAccessibleCount = data.filter(item => item.handicap_accessible === 'Yes').length;


        chartData.value = {
          labels: ['open all year', 'handicap'],
          datasets: [{
            label: '#',
            data: [openYearRoundCount, handicapAccessibleCount],
            backgroundColor: ['#4CAF50', '#FF5733'],
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
  template: '<Doughnut :data="chartData" :options="chartOptions" />'
});

</script>

<style>
.donut{
    width: 30%;
    height: 30%;
    text-align: center;
}
</style>
