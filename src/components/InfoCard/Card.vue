<template>
    <!-- <div v-bind:class="info-card info-card--pink info-card--big"> -->
      <div v-bind:class="className">
        <div class="info-card__title">{{ card.name }}</div>
        <div class="info-card__value">{{ card.value }}</div>
    </div>
</template>

<script>
export default {
  props: ['className', 'card'],  
  data () {
    return {
      msg: 'Welcome to Your Vue.js App'
    }
  }
  
}
</script>

<style lang="scss">

</style>
