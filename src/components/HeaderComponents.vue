<template>
    <header>
        <div class="logo d-flex align-items-center p-4">
            <img src="@/assets/img/spotify1_logo.png" width="50" alt="">
        </div>
    </header>
</template>


<script>
import '@/assets/scss/style.scss'
export default {
    name:"HeaderComponents"
}
</script>

<style lang="scss" scoped>
header{
    height: 10vh;
    background-color: rgba(46, 58, 70, 1);
}

.logo{
    height: 100%;
    
}
</style>