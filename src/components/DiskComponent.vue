<template>
  <div class="container">
    <div class="card d-flex align-items-center">
      <div class="col-7">
        <img :src="disk.poster" alt="" />
        
        <h2 class="white">{{ disk.title }}</h2>
        <div class="center">
          <h4>{{ disk.author }}</h4>
          <h4>{{ disk.year }}</h4>
        </div>
      </div>
    </div>
  </div>
</template>


<script>
export default {
  name: "DiskComponent",
  props: {
    disk: Object,
  },

  mounted() {
    console.log(this.disk);
  },
};
</script>


<style lang="scss" scoped>
.container {
  padding: 20px;
}
img {
  display: inline-block;
  width: 100%;
}

.card {
  background-color: rgba(46, 58, 70, 1);
  min-height: 100%;
  .white{
      color:white;
      font-size: 40px;
  }
}
</style>