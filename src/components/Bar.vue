<script>
import { Bar, mixins }  from 'vue-chartjs'
import ChartJSPluginDatalabels from "chartjs-plugin-datalabels";

export default {  
  extends: Bar,
  props: ['chartData'],
  watch: {
	  chartData:function() { 
		  const data = this.dataSet;
		  data.datasets[0].data = this.chartData.studentsAmount.reverse();
		  data.datasets[1].data = this.chartData.inCampus.reverse();
		  data.labels = this.chartData.groupLabels.reverse();
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
	  const dataSet =  {
		// labels: ["אריאל", "גליל", "גלעד" , "לירז", "ליאב", "זאב"],
		labels: this.chartData.groupLabels.reverse(),
		datasets: [{
			label: 'מספר הילדים בפנימייה',
			data: this.chartData.studentsAmount.reverse(),
			backgroundColor: [
			  '#E5F7FD',
			  '#E5F7FD',
			  '#E5F7FD',
			  '#E5F7FD',
			  '#E5F7FD',
			  '#E5F7FD'
			],
			borderColor: [
			  '#00ACE9',
			  '#00ACE9',
			  '#00ACE9',
			  '#00ACE9',
			  '#00ACE9',
			  '#00ACE9'
			],
			hoverBackgroundColor: ['#00ACE9', '#00ACE9', '#00ACE9', '#00ACE9', '#00ACE9', '#00ACE9'],
			borderWidth: 1,
			categoryPercentage: 0.5,
            barPercentage: 1
		  },
		  {
			label: 'מספר הילדים בבית הספר',
			data: this.chartData.inCampus.reverse(),
			backgroundColor: [
			  '#FFEFF3',
			  '#FFEFF3',
			  '#FFEFF3',
			  '#FFEFF3',
			  '#FFEFF3',
			  '#FFEFF3'
			],
			borderColor: [
			  '#FB6186',
			  '#FB6186',
			  '#FB6186',
			  '#FB6186',
			  '#FB6186',
			  '#FB6186'
			],
			borderWidth: 1,
			hoverBackgroundColor: ['#FB6186', '#FB6186', '#FB6186','#FB6186','#FB6186','#FB6186'],
		    categoryPercentage: 0.5,
            barPercentage: 1
		  }
		]
	}
	  const opt = {
		responsive: true,
		maintainAspectRatio: false,
		tooltips: {
			enabled: false
	   	},
		legend: {
			display: false
		},
		cutoutPercentage: this.cutoutPercentage,
		maintainAspectRatio: false,
		plugins: {
			datalabels: {
				display: true,
				align: 'center',
				color: '#9A9FB3',
				font: {
				size: 14,
				}
			},
		},
		// scales: {
		// 	yAxes: [{
		// 	  stacked: true,
		// 	  ticks: {
		// 		beginAtZero: true
		// 	  }
		// 	}],
		// 	xAxes: [{
		// 	  stacked: true,
		// 	  ticks: {
		// 		beginAtZero: true
		// 	  },
		// 	}]
	  
		// }
		}
		this.dataSet = dataSet;
	  	this.renderChart(dataSet, opt)
    
  },
}
</script>

<style lang="scss">

</style>
