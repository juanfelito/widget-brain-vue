<template>
  <v-container>
    <h2>OPEN</h2>
    <BarChart v-bind:chartdata="openChartData" v-bind:options="chartOptions" />
    <v-divider class="chart-separator"></v-divider>

    <h2>CLOSE</h2>
    <BarChart v-bind:chartdata="closeChartData" v-bind:options="chartOptions" />
  </v-container>
</template>

<script>
import BarChart from './BarChart.vue'

export default {
  data: () => ({
    rawData: [],
    chartOptions: {
      responsive: true,
      maintainAspectRatio: false,
      legend: {
        position: 'top',
        labels: {
          boxWidth: 15,
          usePointStyle: true
        }
      },
      scales: {
        xAxes: [{
          stacked: true,
          scaleLabel: {
            display: true,
            labelString: 'Valve position'
          },
          ticks: {
            min: 0
          }
        }],
        yAxes: [{
          stacked: true,
          scaleLabel: {
            display: true,
            labelString: 'Required torque [%]'
          },
          ticks: {
            min: 0
          }
        }]
      }
    }
  }),
  created() {
    this.requestData()
  },
  computed: {
    positions: function() {
      return Array.from(Array(100).keys());
    },
    openData: function() {
      return this.rawData.filter(function(elem) {
        return elem.Direction == "Open" && elem.Profile === 0;
      })
    },
    openAverage: function() {
      return this.openData.map((elem) => {
        return elem.AverageTorque
      })
    },
    openLastTorque: function() {
      return this.openData.map((elem) => {
        return elem.LastTorque
      })
    },
    openAverageSet1: function() {
      return this.openAverage.slice(0, 100)
    },
    openAverageSet2: function() {
      return this.openAverage.slice(100, 200)
    },
    openLastTorqueSet1: function() {
      return this.openLastTorque.slice(0, 100)
    },
    openLastTorqueSet2: function() {
      return this.openLastTorque.slice(100, 200)
    },
    closeData: function() {
      return this.rawData.filter(function(elem) {
        return elem.Direction == "Close" && elem.Profile === 0;
      })
    },
    closeAverage: function() {
      return this.closeData.map((elem) => {
        return elem.AverageTorque
      })
    },
    closeLastTorque: function() {
      return this.closeData.map((elem) => {
        return elem.LastTorque
      })
    },
    closeAverageSet1: function() {
      return this.closeAverage.slice(0, 100)
    },
    closeAverageSet2: function() {
      return this.closeAverage.slice(100, 200)
    },
    closeLastTorqueSet1: function() {
      return this.closeLastTorque.slice(0, 100)
    },
    closeLastTorqueSet2: function() {
      return this.closeLastTorque.slice(100, 200)
    },
    openChartData: function() {
      return {
        labels: this.positions,
        datasets: [{
          label: 'Average open torque',
          backgroundColor: '#1976d2',
          data: this.openAverageSet1,
          stack: 'average'
        },{
          label: 'Average open torque',
          backgroundColor: '#1e88e5',
          data: this.openAverageSet2,
          stack: 'average'
        },{
          label: 'Last open torque',
          backgroundColor: '#607d8b',
          data: this.openLastTorqueSet1,
          stack: 'last'
        },{
          label: 'Last open torque',
          backgroundColor: '#90a4ae',
          data: this.openLastTorqueSet2,
          stack: 'last'
        }]
      }
    },
    closeChartData: function() {
      return {
        labels: this.positions,
        datasets: [{
          label: 'Average close torque',
          backgroundColor: '#1976d2',
          data: this.closeAverageSet1,
          stack: 'average'
        },{
          label: 'Average close torque',
          backgroundColor: '#1e88e5',
          data: this.closeAverageSet2,
          stack: 'average'
        },{
          label: 'Last close torque',
          backgroundColor: '#607d8b',
          data: this.closeLastTorqueSet1,
          stack: 'last'
        },{
          label: 'Last close torque',
          backgroundColor: '#90a4ae',
          data: this.closeLastTorqueSet2,
          stack: 'last'
        }]
      }
    }
  },
  methods: {
    requestData: function() {
      const that = this
      fetch('http://wb-predictivemaintenance-api.prsp7vkew2.eu-central-1.elasticbeanstalk.com/api/TorqueValues')
      .then(function(response) {
        return response.json();
      })
      .then(function(json) {
        that.rawData = json
      })
    }
  },
  components: {
    BarChart
  }
}
</script>
<style>
  canvas {
    height: 500px;
  }
  .chart-separator {
    margin: 25px 0;
  }
</style>
