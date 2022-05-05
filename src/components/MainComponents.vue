<template>
    <main>
        <AlbumList>
            
        </AlbumList>
    </main>
</template>


<script>
import AlbumList from '@/components/AlbumList.vue';

export default {
    name: "MainComponent",
    methods : {

    },
    components: {
        AlbumList
    }
    
}
</script>


<style lang="scss" scoped>
main{
    height: calc(100vh - 10vh);
    background-color:rgba(30, 45, 59, 1);
}
</style>