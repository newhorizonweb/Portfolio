


<template>

    <div class="project-modal glass-tile">

        <div class="close-modal"
            @click="$emit('hideModals')">

            X
        </div>

         <p>{{ data.title }}</p>

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
        "hideModals"
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

    /* Modal */

.dev-projects .project-modal{
    width:100%;
    height:100%;

    position:absolute;
    top:0;
    left:0;

    opacity:0;
    background:linear-gradient(to bottom right,
        var(--colorBg2e), var(--colorBg2f)),
        url("../../assets/img/noise-texture.svg");

    transition:all 0.75s ease-in-out,
        opacity var(--trans3);
    pointer-events:none;

        /* Modal Content */

    & .close-modal{
        padding:24px;
        background-color:#AAA;
    }

}

    /* Modal Visibility */

.dev-projects{

    & .tile-modal .project-modal{
        width:100vw;
        height:100vh;

        border-radius:0;
        pointer-events:all;

        &:before{
            border-radius:0;
        }

    }

    & .modal-opacity .project-modal{
        opacity:1;
    }

}

</style>