<template>
    <div class="panel panel--content-between panel--grow">
        <div class="panel__inner">
            <div class="panel__header">
                תמונת מצב כללית של הכפר
            </div>
            <div class="chart chart--big">
                <Doughnut v-bind:chartData="prepareData" v-bind:cutoutPercentage="60" />
                <div class="chart__content">
                    <div class="chart__value">
                        {{ getStudentsAmount() }}
                    </div>
                    <div class="chart__title">סה״כ תלמידים בכפר</div>
                </div>
            </div>
            <ul class="chart-legend chart-legend--two-colums">
                <li class="chart-legend__item">
                    <div class="chart-legend__item-indicator" style="background-color: #00ACE9;"></div>
                    <div class="chart-legend__item-title">בכפר</div>
                    <div class="chart-legend__item-value">{{ getStudentsInCampus() }}</div>
                </li>
                <li class="chart-legend__item">
                    <div class="chart-legend__item-indicator" style="background-color: #FFDA23;"></div>
                    <div class="chart-legend__item-title">בחופשה</div>
                    <div class="chart-legend__item-value">{{ getActivity() }}</div>
                </li>
                <li class="chart-legend__item">
                    <div class="chart-legend__item-indicator" style="background-color: #D08CE8;"></div>
                    <div class="chart-legend__item-title">בפעילות חוץ כפרית</div>
                    <div class="chart-legend__item-value">{{ getBanned() }}</div>
                </li>
                <li class="chart-legend__item">
                    <div class="chart-legend__item-indicator" style="background-color: #FB6186;"></div>
                    <div class="chart-legend__item-title">מושהים</div>
                    <div class="chart-legend__item-value">{{ getOffStudy() }}</div>
                </li>
                <li class="chart-legend__item">
                    <div class="chart-legend__item-indicator" style="background-color: #2DE5B9;"></div>
                    <div class="chart-legend__item-title">בטיפול רפואי חוץ</div>
                    <div class="chart-legend__item-value">{{ getIll() }}</div>
                </li>
            </ul>
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
		groupsData: [10, 22, 12, 16, 9],
    }
  },
  methods: {
      getResult() {
          const result = this.prepareData.reduce((acc, el) => {
                acc += Number.isNaN(el) ? 0 : el;
                return acc;
          }, 0);
          return Nubmer.isNaN(parseIntresult);
      },
      getStudentsAmount() {
          if(this.groups && !this.groups.length) {
              return 121
          }
          const result = this.groups.reduce((acc, el) => {
                acc += Number.isNaN(parseInt(el.studentsAmount)) ? 0 : parseInt(el.studentsAmount);
                return acc;
          }, 0);
          return result;
      },
      getOffStudy() {
          if(this.groups && !this.groups.length) {
              return 12
          }
          const result = this.groups.reduce((acc, el) => {
                acc += Number.isNaN(parseInt(el.offStudy)) ? 0 : parseInt(el.offStudy);
                return acc;
          }, 0);
          return result;
      },
      getOnStudy() {
          if(this.groups && !this.groups.length) {
              return 12
          }
          const result = this.groups.reduce((acc, el) => {
                acc += Number.isNaN(parseInt(el.onStudy)) ? 0 : parseInt(el.onStudy);
                return acc;
          }, 0);
          return result;
      },
      getActivity() {
          if(this.groups && !this.groups.length) {
              return 9
          }
          const result = this.groups.reduce((acc, el) => {
                acc += Number.isNaN(parseInt(el.activity)) ? 0 : parseInt(el.activity);
                return acc;
          }, 0);
          return result;
      },
      getIll() {
          if(this.groups && !this.groups.length) {
              return 22
          }          
          const result = this.groups.reduce((acc, el) => {
                acc += Number.isNaN(parseInt(el.ill)) ? 0 : parseInt(el.ill);
                return acc;
          }, 0);
          return result;
      },
      getStudentsInCampus() {
          if(this.groups && !this.groups.length) {
              return 10
          }          
          const result = this.groups.reduce((acc, el) => {
                acc += Number.isNaN(parseInt(el.inCampus)) ? 0 : parseInt(el.inCampus);
                return acc;
          }, 0);
          return result;
      },
       getBanned() {
          if(this.groups && !this.groups.length) {
              return 16
          }
          const result = this.groups.reduce((acc, el) => {
                acc += Number.isNaN(parseInt(el.banned)) ? 0 : parseInt(el.banned);
                return acc;
          }, 0);
          return result;
      },
  },
  computed: {
       prepareData () {
          const data = {
              studentsAmount: 0,
              offStudy: 0,
              activity: 0,
              ill: 0,
              banned: 0,
              onStudy: 0,
              inCampus: 0,
          }
          let result = this.groupsData;
          if(this.groups && this.groups.length) {

            this.groups.reduce((acc, el) => {
                acc.inCampus = acc.inCampus + (Number.isNaN(parseInt(el.inCampus)) ? 0 : parseInt(el.inCampus));
                acc.studentsAmount = acc.studentsAmount + (Number.isNaN(parseInt(el.studentsAmount)) ? 0 : parseInt(el.studentsAmount));
                acc.offStudy = acc.offStudy + (Number.isNaN(parseInt(el.offStudy)) ? 0 : parseInt(el.offStudy));
                acc.activity = acc.activity + (Number.isNaN(parseInt(el.activity)) ? 0 : parseInt(el.activity));
                acc.ill = acc.ill + (Number.isNaN(parseInt(el.ill)) ? 0 : parseInt(el.ill));
                acc.banned = acc.banned + (Number.isNaN(parseInt(el.banned)) ? 0 : parseInt(el.banned));
                acc.onStudy = acc.onStudy + (Number.isNaN(parseInt(el.onStudy)) ? 0 : parseInt(el.onStudy));
                return acc;
            }, data);
            result = [ data.inCampus || undefined, data.offStudy || undefined, data.activity || undefined, data.ill || undefined, data.banned || undefined]
        } 
        return result ;
      }
      
      
  }
  
}
</script>

<style lang="scss">

</style>
