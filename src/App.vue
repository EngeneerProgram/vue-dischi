<template>
  <div id="app">
    <HeaderComponents></HeaderComponents>
    <MainComponents></MainComponents>
  </div>
</template>

<script>
import MainComponents from '@/components/MainComponents.vue'
import HeaderComponents from '@/components/HeaderComponents';
import '@/assets/scss/style.scss';
export default {
  name: 'App',
  components: {
   HeaderComponents,
   MainComponents
  }
}
</script>


