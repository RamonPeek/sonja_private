<template>
  <div>
    <polar-area :data="chartData" :options="chartOptions"></polar-area>
  </div>
</template>

<script>
import { PolarArea } from 'vue-chartjs';
import {
Chart as ChartJS,
CategoryScale,
LinearScale,
PointElement,
LineElement,
Title,
Tooltip,
Legend,
TimeScale,
RadialLinearScale,
ArcElement
} from 'chart.js';

export default {
  components: {
    PolarArea
  },
  created() {
    ChartJS.register(
 CategoryScale,
 LinearScale,
 PointElement,
 LineElement,
 TimeScale,
 RadialLinearScale,
 ArcElement,
 Title,
 Tooltip,
 Legend
);
  },
  data() {
    return {
      chartData: {
        datasets: [{
          data: [1,2,3,4,5,5,4,3,2,1,1,2,3,4,5,5,4,3,2,1,1,2,3,4,5,5,4,3,2,1,1,2,3,4,5,5,4,3,2,1,1,2,3,4,5,5,4,3,2,1], // Sample data for progress in percentage
          backgroundColor: [
            'rgba(255, 99, 132, 0.5)',
            'rgba(54, 162, 235, 0.5)',
            'rgba(255, 206, 86, 0.5)',
            'rgba(75, 192, 192, 0.5)',
            'rgba(153, 102, 255, 0.5)'
          ],
          borderColor: [
            'rgba(255,99,132,1)',
            'rgba(54, 162, 235, 1)',
            'rgba(255, 206, 86, 1)',
            'rgba(75, 192, 192, 1)',
            'rgba(153, 102, 255, 1)'
          ],
          borderWidth: 1
        }]
      },
      chartOptions: {
        // Customize options as per your requirement
        // For example:
        responsive: true,
        maintainAspectRatio: false,
      }
    };
  }
};
</script>
