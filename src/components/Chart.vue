<script>
import {Line} from 'vue-chartjs'

export default {
  name: 'myChart',
  extends: Line,
  props: {
    dataset: {
      type: Array,
      default: null
    },
    labels: {
      type: Array,
      default: null
    }
  },
  data() {
    return {
      chartData: {
        labels: this.labels,
        datasets: [
          {
            label: 'Line Chart',
            data: this.dataset[0],
            borderColor: '#2554FF',
            backgroundColor: '#2554FF',
            borderWidth: 1,
          },
          {
            label: 'Line Chart',
            data: this.dataset[1],
            borderColor: 'red',
            backgroundColor: 'red',
            borderWidth: 1
          }
        ]
      },
      options: {
        scales: {
          yAxes: [{
            ticks: {
              beginAtZero: true
            },
            gridLines: {
              display: true
            }
          }],
          xAxes: [{
            gridLines: {
              display: false
            }
          }]
        },
        legend: {
          display: true
        },
        responsive: true,
        maintainAspectRatio: false
      }
    }
  },
  mounted() {
    this.renderChart(this.chartData, this.options)
  }

}
</script>