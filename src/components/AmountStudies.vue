<template>
    <div class="panel panel--55 panel--grow">
        <div class="panel__inner">
            <div class="panel__header">
                מספר תלמידים בבית הספר
            </div>
            <div class="chart chart--height">
                <Bar v-bind:chartData="prepareData"  />
            </div>
            <!-- <ul class="chart-legend chart-legend--center chart-legend--mt">
                <li class="chart-legend__item">
                    <div class="chart-legend__item-indicator" style="background: #E5F7FD;border: 1px solid #00ACE9;"></div>
                    <div class="chart-legend__item-title">מספר הילדים בפנימייה</div>
                </li>
                <li class="chart-legend__item">
                    <div class="chart-legend__item-indicator" style="background: #FFEFF3; border: 1px solid #FB6186;"></div>
                    <div class="chart-legend__item-title">מספר הילדים בבית הספר</div>
                </li>
            </ul> -->
        </div>
    </div>
</template>

<script>
import Bar from './Bar.vue'
export default {  
  components: { Bar }, 
  props: ['groups'],
  data () {
    return {
      msg: 'Welcome to Your Vue.js App'
    }
  },
  computed: {
       prepareData () {
          const data = {
              studentsAmount: [],
              inCampus: [],
              groupLabels: []
          }
          if(this.groups && this.groups.length) {

            const result = this.groups.reduce((acc, el) => {
                acc.studentsAmount.push(parseInt(el.studentsAmount));
                acc.inCampus.push(parseInt(el.inCampus));
                acc.groupLabels.push(el.groupName);
                return acc;
            }, data);
            return result;
        } 
        return  {
              studentsAmount: [15, 27, 18, 28, 27, 20],
              inCampus: [4, 5, 1, , 5, 9],
              groupLabels: ["אריאל", "גליל", "גלעד" , "לירז", "ליאב", "זאב"],
          } ;
      }
  }
  
}
</script>

<style lang="scss">

</style>
