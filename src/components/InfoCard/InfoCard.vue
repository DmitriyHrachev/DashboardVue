<template>
<div class="info">
    <div class="info__col">
        <Card v-bind:card="cards.infoCard" :className="'info-card info-card--pink info-card--big'" />
    </div>
    <div class="info__col">
        <Card v-bind:card="cards.infoCard2" :className="'info-card info-card--blue'" />
        <Card v-bind:card="cards.infoCard3" :className="'info-card info-card--yellow'" />
    </div>
</div>
</template>

<script>
import Card from './Card.vue'
export default {
  components: { Card },
  props: ["cards"],  
  data () {
    return {
      msg: 'Welcome to Your Vue.js App'
    }
  }
  
}
</script>

<style lang="scss">

</style>
