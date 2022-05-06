<template>
  <header>
    <div class="logo d-flex align-items-center p-4">
      <img src="@/assets/img/spotify1_logo.png" width="50" alt="" />
    </div>

     <form class="d-flex">
        <input class="form-control me-2" type="search" v-model="search" placeholder="Search" aria-label="Search">
        <button class="btn btn-outline-success" type="submit">Search</button>
      </form>
      
  </header>
</template>


<script>
import "@/assets/scss/style.scss";
export default {
  name: "HeaderComponents",
  data(){
      return {
          gener: [],
          search:""
      }

  },
  
  
 

};
</script>

<style lang="scss" scoped>
header {
  background-color: rgba(46, 58, 70, 1);
  display: Flex;
  justify-content: space-between;
  align-items:center;
}

.logo {
  height: 100%;
}
.form{
    height: 100%;
}
input{
    width: 150px;
    height: 40px;
}

.btn{
    width: 100px;
    height: 40px;
}
</style>