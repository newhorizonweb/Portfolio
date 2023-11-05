


<template>

    <div class="tile-modal">
        <div class="tile-modal-inner hide-scrollbar"
            ref="innerModal">

            <TileDisplay
                :data="data"
            />

            <CloseBtn
                :glassTile="true"
                @click="
                    scrollTopModal(),
                    $emit('hideModals')
                "
            />

            <div class="modal-content wrapper">

                <div class="project-overview glass-tile">
                    <h3 class="project-heading" data-text="Overview"></h3>

                    <div class="desc-elem-inner">
                        <p v-for="(paragraph, index) in data.overview" :key="index">
                            {{ paragraph }}
                        </p>
                    </div>
                </div>

                <ProjectMockup
                    :data="data"
                />

                <div class="project-desc">

                    <div class="desc-elem project-about glass-tile">
                        <h3 class="project-heading" data-text="About"></h3>

                        <div class="desc-elem-inner">
                            <p v-for="(paragraph, index) in data.about" :key="index">
                                {{ paragraph }}
                            </p>
                        </div>
                    </div>

                    <div class="desc-elem project-stack glass-tile">
                        <h3 class="project-heading" data-text="stack"></h3>

                        <div class="desc-elem-inner">
                            <p v-for="(paragraph, index) in data.stack" :key="index">
                                {{ paragraph }}
                            </p>
                        </div>
                    </div>

                </div>

            </div>

        </div>
    </div>

</template>



<script lang="ts">
import { defineComponent } from 'vue';
import CloseBtn from "../pageElements/CloseBtn.vue";

import TileDisplay from "./TileDisplay.vue";
import ProjectMockup from "./ProjectMockup.vue";

export default defineComponent({
    name: "ProjectModal",

    components:{
        CloseBtn,
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

        scrollTopModal(){

            const innerModal = this.$refs.innerModal as HTMLElement;
            innerModal.scrollTo({
                top:0,
                behavior:"smooth"
            });
            
        }

    }

});
</script>



<style lang="scss">

    /* Modal */

.tile-section .tile-modal{
    width:100%;
    height:100%;

    position:absolute;
    top:0;
    left:0;

    transition:all 0.75s ease-in-out,
        opacity var(--trans3);
        
    overflow:hidden;
    pointer-events:none;

    &:after{
        content:"";
        width:100%;
        height:100%;

        position:absolute;
        top:0;
        left:0;

        opacity:0;
        background:var(--colorGrad1b);
        
        transition:0.25s ease-in-out;
        z-index:-1;
    }

    & .tile-modal-inner{
        width:100%;
        height:100%;
        padding:0 var(--size6);
        overflow:auto;
    }

    & .close-btn{
        position:absolute;
        top:var(--size6);
        right:var(--size6);
        opacity:0;
    }

        /* Modal Content */

    & .modal-content{
        width:100vw;
        padding-bottom:var(--size8);
        
        display:flex;
        flex-direction:column;
        gap:var(--size8);
        transition:1s;
    }

    & .project-heading{
        text-align:center;
        margin-bottom:var(--size6);
        text-transform:capitalize;

        &:before{
            -webkit-text-stroke-color:var(--color1a);
        }

    }

    & .project-overview{
        padding:var(--size8) var(--size6);
        
        & p{
            text-align:center;
        }

    }

    & .desc-elem-inner{
        display:flex;
        flex-direction:column;
        gap:var(--size3);
    }

    & .project-desc{
        display:flex;
        flex-wrap:wrap;
        align-items:flex-start;
        gap:var(--size8);

        & .desc-elem{
            padding:var(--size8) var(--size6);
            transition:0s;
        }

        & .project-about{
            flex:1;
        }

        & .project-stack{
            width:260px;

            & p{
                text-align:center;
            }

        }

    }

}

    /* Modal Visibility Modes */

.tile-section{

    & .tile-modal-open .tile-modal{
        width:100vw;
        height:100vh;

        border-radius:0;
        pointer-events:all;

        &:before{
            border-radius:0;
        }

        & .close-btn{
            opacity:1;
        }

        & .modal-content{
            width:min(1024px, 100%);
        }

    }

    & .modal-opacity .tile-modal{

        &:after{
            opacity:1;
        }

    }

    & .no-trans .tile-modal{
        transition:0s;
    }

}

@media screen and (width <= 1024px){

    .tile-section .tile-modal{

        & .project-desc{
            display:flex;
            gap:var(--size8);

            & > div{
                flex:100%;
                width:auto;
            }

        }

    }

}

</style>