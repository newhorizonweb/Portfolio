


<template>

    <div class="project-modal glass-tile">
        <div class="project-modal-inner hide-scrollbar">

            <TileDisplay
                :data="data"
            />

            <div class="close-modal glass-tile"
                @click="$emit('hideModals')">

                <span></span>
                <span></span>
            </div>

            <div class="modal-content wrapper">

                <ProjectMockup
                    :data="data"
                />

            </div>

        </div>
    </div>

</template>



<script lang="ts">
import { defineComponent } from 'vue';

import TileDisplay from "../main/TileDisplay.vue";
import ProjectMockup from "../main/ProjectMockup.vue";

export default defineComponent({
    name: "ProjectModal",

    components:{
        TileDisplay,
        ProjectMockup
    },

    props:[
        "data"
    ],

    emits:[
        "hideModals"
    ],

    data(){
        return{
            desktopMockup: false
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
    padding:0 var(--size6);

    position:absolute;
    top:0;
    left:0;

    background:linear-gradient(to bottom right,
        var(--colorBg2e), var(--colorBg2f)),
        url("../../assets/img/noise-texture.svg");

    transition:all 0.75s ease-in-out,
        opacity var(--trans3);
        
    overflow:hidden;
    pointer-events:none;

    & .project-modal-inner{
        width:100%;
        height:100%;
        overflow-x:auto;
    }

    & .close-modal{
        width:var(--size7);
        aspect-ratio:1/1;

        position:absolute;
        top:var(--size6);
        right:var(--size6);

        opacity:0;
        z-index:120;

        & span{
            width:var(--size5);
            height:2px;

            position:absolute;
            top:50%;
            left:50%;
            transform:translate(-50%, -50%) rotate(45deg);

            background-color:var(--color1a);
            border-radius:200px;
        }

        & span:nth-of-type(2){
            transform:translate(-50%, -50%) rotate(-45deg);
        }

    }

        /* Modal Content */

    & .modal-content{
        padding-bottom:var(--size8);
    }

}

    /* Modal Visibility Modes */

.dev-projects{

    & .tile-modal .project-modal{
        width:100vw;
        height:100vh;

        border-radius:0;
        pointer-events:all;

        &:before{
            border-radius:0;
        }

        & .close-modal{
            opacity:1;
        }

    }

    & .no-trans .project-modal{
        transition:0s;
    }

}

</style>