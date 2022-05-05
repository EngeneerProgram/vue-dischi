<template>
  <div class="container">
    <div class="card d-flex align-items-center">
      <div class="col-7">
        <img class="mt-4" :src="disk.poster" alt="" />
        <div class="title_container">
            <h2 class="white text-center">{{ disk.title }}</h2>
        </div>
        <div class="center text-center">
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
      
  }

  .title_container{
      width: 130px;
      
  }
}
</style>