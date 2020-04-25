<script>
  import { Line } from 'vue-chartjs'
  
  export default {
    extends: Line,
    props: {
      chartData: {
        // eslint-disable-next-line vue/require-prop-type-constructor
        type: Array | Object,
        required: false
      },
      chartLabels: {
        type: Array,
        required: true
      }
    },
    data () {
      return {
        gradient: null,
        options: {
          showScale: true,
          scales: {
            yAxes: [{
              ticks: {
                beginAtZero: false,
                fontSize: 20
              },
              gridLines: {
                display: false,
              }
            }],
            xAxes: [ {
              scaleLabel:{
                fontSize: 40
              },
              ticks: {
                fontSize: 20
              },
              gridLines: {
                display: true,
                color: '#ececf0',
                type: 'linear'
              },
            }]
          },
          legend: {
            display: false,
          },
          responsive: true,
          maintainAspectRatio: false,
        },
        window: {
            width: 0,
            height: 0
        },
        timoutHandle: null
      }
      
    },

    created() {
        window.addEventListener('resize', this.handleResize);
        this.handleResize();
    },
    destroyed() {
        window.removeEventListener('resize', this.handleResize);
        this.handleResize();
    },
    mounted () {
      this.$refs.canvas.width = window.width
      this.renderChart({
        labels: this.chartLabels,
        datasets: [
          {
            label: 'Temperature',
            borderColor: '#75d6fc',
            pointBackgroundColor: '#75d6fc',
            pointBorderColor: '#75d6fc',
            pointHoverBorderColor: '#249EBF',
            pointHoverBackgroundColor: '#fff',
            pointHoverRadius: 6,
            pointHitRadius: 10,
            pointHoverBorderWidth: 1,
            borderWidth: 3,
            data: this.chartData,
    
          }
        ]
      }, this.options)
    },
    methods: {
        handleResize() {
            this.window.width = window.innerWidth;
            this.window.height = window.innerHeight;
            
            this.renderChart({
              labels: this.chartLabels,
              datasets: [
                {
                  label: 'Temperature',
                  borderColor: '#75d6fc',
                  pointBackgroundColor: '#75d6fc',
                  pointBorderColor: '#75d6fc',
                  pointHoverBorderColor: '#249EBF',
                  pointHoverBackgroundColor: '#fff',
                  pointHoverRadius: 6,
                  pointHitRadius: 10,
                  pointHoverBorderWidth: 1,
                  borderWidth: 3,
                  data: this.chartData,
          
                }
              ]
            }, this.options)
        }
    }
    
  }
</script>