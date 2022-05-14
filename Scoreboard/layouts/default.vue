<template>
  <v-app dark>
    <Bar
      ref="plot"
      :chart-options="chartOptions"
      :chart-data="getChartData"
      :width="$vuetify.breakpoint.width"
      :height="$vuetify.breakpoint.height"
    />
    <v-btn @click="debugUpdate">debug update</v-btn>
    <v-btn @click="addNewPlayer('Test')">debug update</v-btn>
  </v-app>
</template>

<script>
import {Bar} from "vue-chartjs/legacy"

import {
  Chart as ChartJS,
  Title,
  Tooltip,
  BarElement,
  CategoryScale,
  LinearScale
} from 'chart.js'

ChartJS.register(Title, Tooltip, BarElement, CategoryScale, LinearScale)

export default {
  name: 'DefaultLayout',
  components: {
    Bar
  },
  computed: {
    getChartData() {
      return this.chartData
    }
  },
  data() {
    return {
      chartData: {
        labels: ["Marcin", "Andrzej", "Stefan"],
        datasets: [
          {
            backgroundColor: "#d0417e",
            data: [5, 2, 10],
            borderColor: "#F8BBD0",
            borderWidth: 2,
            hoverBackgroundColor: "#880E4F",
            hoverBorderColor: "#F8BBD0"
          }
        ]
      },
      chartOptions: {
        responsive: true,
        maintainAspectRatio: false,
        plugins: {
          title: {
            display: true,
            text: "Ktoś będzie miał urodziny - tylko kto?",
            font: {size: 24},
            color: "#E3F2FD"
          }
        },
        scales: {
          x: {
            grid: {
              color: "#323232"
            },
            ticks: {
              color: "#E3F2FD",
              font: {size: 16, weight: "bold"}
            }
          },
          y: {
            grid: {
              color: "#323232"
            },
            ticks: {
              color: "#E3F2FD",
              font: {weight: "bold"}
            }
          }
        }
      }
    }
  },
  methods: {
    debugUpdate() {
      this.chartData.datasets[0].data[0] = 12
      this.$refs.plot.updateChart()
    },
    addNewPlayer(playerName) {
      this.chartData.labels.push(playerName)
      this.chartData.datasets[0].data.push(0)
      this.$refs.plot.updateChart()
    }
  }
}
</script>
