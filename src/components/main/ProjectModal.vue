


<template>

    <div class="project-modal">

        <div class="close-modal"
            @click="$emit('closeModal')">

            <p>X</p>
        </div>


        <p>{{ data }}</p>

    </div>

</template>



<script lang="ts">
import { defineComponent } from 'vue';

export default defineComponent({
    name: "ProjectModal",

    props:[
        "data"
    ],

    emits:[
        "closeModal"
    ],

    data(){
        return{


            
        } 
    },

    methods:{



    }

});
</script>



<style lang="scss">

.project-modal{
    width:100%;
    height:100%;

    position:fixed;
    top:0;
    left:0;

    background-color:rgb(200,200,255,0.2);
    z-index:100;
}

.close-modal{
    padding:8px;
    background-color:#999;
}

</style>