<template>
    <div class="select">
        <select
        
         name="genere"
        id="genere"
        :value = 'tipo_genere'
        @input=$emit('input', $event.target.value);
        @change="$emit('selectGenere')"        
        
        >
        
        <option>All</option>
        <option>Rock</option>
        <option>Jazz</option>
        <option>Pop</option>
        <option>Metal</option>
        


        </select>




    </div>
</template>


<script>
export default {
    name: "SelectGender",
    props: {
        tipo_genere : String,
    },
};
</script>