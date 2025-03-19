<template>
  <div>
    <MixedChart :data="chartData" :options="chartOptions" />
  </div>
</template>

<script>
import { ref, onMounted } from 'vue';
import { Line, Bar } from 'vue-chartjs'
import { Chart as ChartJS, Title, Tooltip, Legend, LineElement, BarElement, CategoryScale, LinearScale } from 'chart.js'

// Register necessary components with Chart.js
ChartJS.register(Title, Tooltip, Legend, LineElement, BarElement, CategoryScale, LinearScale)

export default {
  components: {
    MixedChart: Line,  // Using `Line` as the wrapper for the mixed chart component
  },
  data() {
    return {
      // Mixed chart data (combining a Line and Bar chart)
      chartData: {
        labels: ['January', 'February', 'March', 'April', 'May', 'June'],  // X-axis labels
        datasets: [
          {
            type: 'line',
            label: 'Line Dataset',
            data: [65, 59, 80, 81, 56, 55],  // Line data
            borderColor: 'rgba(75, 192, 192, 1)',  // Line color
            backgroundColor: 'rgba(75, 192, 192, 0.2)',  // Line fill color
            fill: true,  // Fill the area below the line
            tension: 0.4, // Line tension (curvature)
            yAxisID: 'y',
          },
          {
            type: 'bar',
            label: 'Bar Dataset',
            data: [40, 60, 50, 30, 70, 90],  // Bar data
            backgroundColor: 'rgba(255, 99, 132, 0.6)',  // Bar color
            yAxisID: 'y1',  // Use a second Y-axis for the bar chart
          },
        ]
      },
      // Mixed chart options
      chartOptions: {
        responsive: true,
        maintainAspectRatio: false,
        scales: {
          x: {
            beginAtZero: true,
          },
          y: {
            beginAtZero: true,
            position: 'left',  // Y-axis for the line chart
          },
          y1: {
            beginAtZero: true,
            position: 'right',  // Y-axis for the bar chart (on the right)
            grid: {
              drawOnChartArea: false,  // Hide grid lines for the second Y-axis
            },
          },
        },
        plugins: {
          legend: {
            position: 'top',
          },
          tooltip: {
            callbacks: {
              label: (tooltipItem) => `${tooltipItem.dataset.label}: ${tooltipItem.raw} units`
            },
          },
        },
      }
    }
  }
}



onMounted(async () => {
  const api = "https://data.cityofnewyork.us/resource/hjae-yuav.json"
  const response = await fetch(api);
  const data = await response.json();
  

})
</script>
