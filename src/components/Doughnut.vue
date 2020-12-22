<script>
import { Doughnut, mixins }  from 'vue-chartjs'
import ChartJSPluginDatalabels from "chartjs-plugin-datalabels";

export default {  
  extends: Doughnut,
  props: ['chartData', 'cutoutPercentage'],
  watch: {
	  chartData:function() { 
		  const data = this.dataSet;
		  data.datasets[0].data = this.chartData;
		  const options = this.opt;
		  this.renderChart(data, options);
	  }
  },
  data () {
    return {
	  dataSet: {},
	  opt: {},
    }
  },
  mounted () {
	  const dataSet = {
		borderWidth: 2,
		datasets: [{
			data: this.chartData,
			datalabels: {
				color: '#000',			
			},
			backgroundColor: [
				'rgba(0, 172, 233, 0.1)',
				'rgba(251, 97, 134, 0.1)',
				'rgba(255, 218, 35, 0.1)',
				'rgba(45, 229, 185, 0.1)',
				'rgba(208, 140, 232, 0.1)'
				],
				borderColor: [
				'#00ACE9',
				'#FB6186',
				'#FFDA23',
				'#2DE5B9',
				'#D08CE8'
				],
				borderWidth: 2,
				hoverBackgroundColor: ['#00ACE9', '#FB6186', '#FFDA23', '#2DE5B9', '#D08CE8'],
		}],
	  }
	  const opt = {
		tooltips: {
			enabled: false
	   	},
		legend: {
			display: false
		},
		
		cutoutPercentage: this.cutoutPercentage,
		maintainAspectRatio: false,
		plugins: {datalabels: {
				display: true,
				align: 'center',
				color: '#9A9FB3',
				font: {
				size: 11,
				}
			}},
    }
		this.dataSet = dataSet;
	  this.renderChart(dataSet, opt)
    
  },
}
</script>

<style lang="scss">

</style>
