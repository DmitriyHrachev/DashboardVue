<template>
    <div class="clock">
        <div class="clock__live">{{hours}}:{{minutes}}:{{seconds}}</div>
        <div class="clock__title">{{ getDate() }}</div>
    </div>
</template>

<script>
export default {  
  mounted() {
    this.$options.timer = window.setTimeout(this.updateDateTime, 1000);
  },
  beforeDestroy() {
    window.clearTimeout(this.$options.timer);
  },
  data () {
    return {
      hours: 0,
      minutes: 0,
      seconds: 0,
    }
  },
  methods: {
    updateDateTime() {
      const now = new Date();
      this.hours = this.getZeroPad(now.getHours());
      this.minutes = this.getZeroPad(now.getMinutes());
      this.seconds = this.getZeroPad(now.getSeconds());
      this.$options.timer = window.setTimeout(this.updateDateTime, 1000);
    },
    getZeroPad (n) {
     return (parseInt(n, 10) >= 10 ? '' : '0') + n
    },
    getDate() {
      const now = new Date();
      return this.getZeroPad(now.getDate()) + "/" + (now.getMonth() + 1) + "/" + now.getFullYear();
    }
  },
  
}
</script>

<style lang="scss">

</style>
