<template>
    <section class="disk">


        <div class="container">

            <div class="row">
                <Disk>
                    :disk="disk"
                    v-for="disk in disks"
                    :key="disk.id"


                </Disk>
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
        disks: null,
        error: null,

        };
    },

    methods : {
        callApi() {
            axios
            .get(this.API_URI)
            .then((response)=>{
                this.disk = response.data;
                
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