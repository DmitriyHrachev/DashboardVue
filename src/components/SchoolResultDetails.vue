<template>
	<div class="panel panel--content-between panel--grow">
		<div class="panel__inner">
			<div class="panel__header">
				נוכחות חניכים לפי קבוצות
			</div>

			<div class="charts">
				<div v-bind:key="group.el.id" v-for="group in prepareData" class="charts__item">
					<div class="charts__item-title">
						{{group.el.groupName}}	
					</div>
					<div class="chart">
						<Doughnut v-bind:chartData="group.dataSet" v-bind:cutoutPercentage="50" />
						<div class="chart__content">
							<div class="chart__value">{{group.result}}</div>
						</div>
					</div>
				</div>
			</div>

			<ul class="chart-legend chart-legend--random">
				<li class="chart-legend__item">
					<div class="chart-legend__item-indicator" style="background-color: #00ACE9;"></div>
					<div class="chart-legend__item-title">בכפר</div>
				</li>
				<li class="chart-legend__item">
					<div class="chart-legend__item-indicator" style="background-color: #FFDA23;"></div>
					<div class="chart-legend__item-title">בחופשה</div>
				</li>
				<li class="chart-legend__item">
					<div class="chart-legend__item-indicator" style="background-color: #D08CE8;"></div>
					<div class="chart-legend__item-title">בפעילות חוץ כפרית</div>
				</li>
				<li class="chart-legend__item">
					<div class="chart-legend__item-indicator" style="background-color: #FB6186;"></div>
					<div class="chart-legend__item-title">מושהים</div>
				</li>
				<li class="chart-legend__item">
					<div class="chart-legend__item-indicator" style="background-color: #2DE5B9;"></div>
					<div class="chart-legend__item-title">בטיפול רפואי חוץ</div>
				</li>
			</ul>

			<table class="table">
				<thead>
					<tr>
						<th>שם הקבוצה</th>
						<th>בכפר</th>
						<th>מחוץ לכפר</th>
					</tr>
				</thead>
				<tbody>
					<tr v-bind:key="group.el.id" v-for="group in prepareData">
						<td>{{group.el.groupName}}</td>
						<td >{{ studentsInCampus(group) }}</td>
						<td>{{studentsOffCampus(group)}}</td>
					</tr>
				</tbody>
				<div class="table__body">
					
				</div>
			</table>

		</div>
	</div>
</template>

<script>
import Doughnut from './Doughnut.vue'
import ChartJSPluginDatalabels from "chartjs-plugin-datalabels";
export default {
components: { Doughnut },  
props: ['groups'],  
  data () {
    return {
	  groupsDataSetMock1: [21, 3, 5, 1],
	  groupsDataSetMock2: [19, 4, 6],
	  groupsDataSetMock3: [20, 1, 2, 3, 7],
	  groupsDataSetMock4: [17, 5, 7, , 2],
	  groupsDataSetMock5: [29, , , 1,],
	  groupsDataSetMock6: [15, 3, 2, 4, 3],
    }
  },
  methods: {
	  studentsOffCampus(group) {
		  if(!group.el.offStudy)  {
			  return 9;
		  }
		  return parseInt(group.el.studentsAmount) - parseInt(group.el.inCampus)
	  },
	  studentsInCampus(group) {
		  if(!group.el.offStudy)  {
			  return 21;
		  }
		  return parseInt(group.el.inCampus)
	  }
  }, 
  computed: {
       prepareData () {
          if(this.groups && this.groups.length) {

            const result = this.groups.reduce((acc, el) => {
				const group = { el }
				group.dataSet = [parseInt(el.inCampus) || undefined, parseInt(el.offStudy) || undefined, parseInt(el.activity) || undefined, parseInt(el.ill) || undefined, parseInt(el.banned) || undefined];
				group.result = group.dataSet.reduce((acc1, el) => {
					acc1 += parseInt(el);
					return acc1;
				}, 0); 
				acc = [...acc, group];  
                return acc;
			}, []);
			return result;
		}
		return [{dataSet: this.groupsDataSetMock1, result: 30,el: {groupName: 'גליל'}},
		{dataSet: this.groupsDataSetMock2, result: 29, el: {groupName: 'גליל'}},
		{dataSet: this.groupsDataSetMock3, result: 33, el: {groupName: 'גליל'}}, 
		{dataSet: this.groupsDataSetMock4, result: 31, el: {groupName: 'גליל'}},
		{dataSet: this.groupsDataSetMock5, result: 30, el: {groupName: 'גליל'}},
		{dataSet: this.groupsDataSetMock6, result: 27, el: {groupName: 'גליל'}}
		] 
	   }
  }
}
</script>

<style lang="scss">

</style>
