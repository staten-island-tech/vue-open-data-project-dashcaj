<template>
  <div>
    <PieChart :data="chartData" :options="chartOptions" />
  </div>
</template>

<script>
import { Pie } from 'vue-chartjs'
import { Chart as ChartJS, Title, Tooltip, Legend, ArcElement, CategoryScale, LinearScale } from 'chart.js'

// Register the necessary components with Chart.js
ChartJS.register(Title, Tooltip, Legend, ArcElement, CategoryScale, LinearScale)

export default {
  components: {
    PieChart: Pie
  },
  data() {
    return {
      // Chart data
      chartData: {
        labels: ['Red', 'Blue', 'Green'],  // Labels for each slice of the pie
        datasets: [
          {
            label: 'My Pie Chart',
            data: [1, 2, 3],  // Values for each slice
            backgroundColor: ['red', 'blue', 'green'],  // Colors for each slice
            hoverOffset: 4
          }
        ]
      },
      // Chart options
      chartOptions: {
        responsive: true,
        maintainAspectRatio: false,
        plugins: {
          legend: {
            position: 'top'
          },
          tooltip: {
            callbacks: {
              label: (tooltipItem) => {
                return `${tooltipItem.label}: ${tooltipItem.raw} units`
              }
            }
          }
        }
      }
    }
  }
}
</script>
