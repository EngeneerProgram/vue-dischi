<template>
  <div id="app">
    <HeaderComponents></HeaderComponents>
    <AlbumList></AlbumList>
  </div>
</template>

<script>
// import MainComponents from '@/components/MainComponents.vue'

import AlbumList from '@/components/AlbumList.vue';
import HeaderComponents from '@/components/HeaderComponents';
import '@/assets/scss/style.scss';
export default {
  name: 'App',
  components: {
   HeaderComponents,
  //  MainComponents,
   AlbumList
  }
}
</script>


