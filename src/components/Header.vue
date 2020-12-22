<template>
    <header class="header">
        <div @click="openModal" class="header__btn">
            הזן את הנתונים שלך
            <img src="../assets/icon.svg" alt="">
        </div>
        <a href="" class="header__logo">
            <img src="../assets/logo.svg" alt="">
        </a>
        <a href="" class="header__company">
            <span>smart-</span>campus.co.il
        </a>
    </header>
</template>

<script>
export default {  
  data () {
    return {
      msg: 'Welcome to Your Vue.js App',
      openModal: () => {
          const vm = this;
          vm.$emit('openModal');
      }
    }
  }
  
}
</script>

<style lang="scss">

</style>
