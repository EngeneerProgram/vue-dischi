<template>
    <div class="container">
        <img :src="disk.poster" alt="">
        <h2>{{disk.title}}</h2>
        <div class="center">
            <h3>{{disk.autor}}</h3>
            <h4>{{disk.year}}</h4>
        </div>
    </div>

</template>


<script>
export default {
    name: "DiskComponent",
    props: {
        character : Object
    }
};
</script>


<style lang="scss" scoped>

</style>