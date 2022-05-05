<template>
    <section class="disk">


        <div class="container pt-5">

            <div class="row row-cols-lg-5">
                
                <DiskComponent
                    v-for="disk in disks"
                    :disk="disk"
                    :key="disk.id"
                >

                </DiskComponent>
               
            </div>
        </div>


    </section>
</template>

<script>
import axios from 'axios';
import DiskComponent from '@/components/DiskComponent.vue';

export default {
    name: "AlbumList",
    components: {
        DiskComponent,
    },

    data() {
        return { 

        API_URI : "https://flynn.boolean.careers/exercises/api/array/music",
        disks: [],
        error: null,

        };
    },

    methods : {
        callApi() {
            axios
            .get(this.API_URI)
            .then((response)=>{
                console.log(response.data.response);
                this.disks = response.data.response;
                
            })
            .catch((error)=>{
                console.error();
                error;
                this.error = `Ci sono dei problemi`
                
            });
        }
    },
    mounted(){
        this.callApi();
    },
};
</script>


<style lang="scss">
.disk{
    background-color: rgba(30, 45, 59, 1);

    
}
</style>