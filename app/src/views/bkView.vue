<template>
  <Bar
    id="my-chart-id"
    :options="chartOptions"
    :data="chartData"
  />
</template>

<script>
import { Doughnut } from 'vue-chartjs'
import { Chart as ChartJS, Title, Tooltip, Legend, ArcElement } from 'chart.js'

// Register the necessary components in Chart.js
ChartJS.register(Title, Tooltip, Legend, ArcElement)

export default {
  components: {
    Doughnut
  },
  data() {
    return {
      // Data for the Doughnut chart
      chartData: {
        labels: ['Red', 'Blue', 'Yellow'], // Labels for segments
        datasets: [
          {
            data: [300, 50, 100], // Data values for the chart
            backgroundColor: ['#FF5733', '#3498DB', '#F1C40F'], // Colors for segments
            hoverBackgroundColor: ['#FF6347', '#5DADE2', '#F39C12']
          }
        ]
      },
      chartOptions: {
        responsive: true, // Make it responsive
        plugins: {
          legend: {
            position: 'top', // Position of the legend
          },
          tooltip: {
            enabled: true // Enable tooltips
          }
        }
      }
    }
  }
}
</script>
