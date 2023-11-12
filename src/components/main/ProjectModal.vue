


<template>

    <div class="tile-modal">
        <div class="tile-modal-inner hide-scrollbar"
            ref="innerModal">

            <TileDisplay
                :data="data"
            />

            <div class="modal-hub">

                <a :href="data.gitHubLink" target="_blank"
                    aria-label="Project GitHub Repository Link"
                    class="modal-hub-link mh-link1" v-if="data.gitHubLink">
                    
                    <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 200 200"><path class="anim-elem1 cls-1" d="M82.6,144.3c-21.1-2.4-43.2-10.5-43.2-46.9a36,36,0,0,1,9.8-25.5,33.5,33.5,0,0,1,.9-25.1s7.9-2.6,26.1,9.7a89.1,89.1,0,0,1,47.5,0c18.1-12.3,26.1-9.7,26.1-9.7a34,34,0,0,1,.9,25.1,36.8,36.8,0,0,1,9.8,25.5c0,36.4-22.1,44.4-43.3,46.8"/><path class="cls-1" d="M117.2,144.2a22.7,22.7,0,0,1,6.4,17.7v26c0,3.2,1.7,5.5,6.5,4.5a95.1,95.1,0,1,0-60.1,0c4.7.9,6.5-2,6.5-4.4V171.9c-26.5,5.7-32-12.8-32-12.8a25.4,25.4,0,0,0-10.7-14c-8.7-5.9.6-5.8.6-5.8a19.4,19.4,0,0,1,14.5,9.8c8.5,14.5,22.1,10.3,27.7,7.9a20.5,20.5,0,0,1,6-12.7"/></svg>
                </a>
                
                <a :href="data.pageLink" target="_blank"
                    aria-label="Hosted Project Link"
                    class="modal-hub-link mh-link2" v-if="data.pageLink">

                    <svg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 200 200'><circle class='cls-1' cx='100' cy='100' r='95'/><path class='cls-1 anim-elem2' d='M100,195c29.4,0,53.2-42.5,53.2-95S129.4,5,100,5'/><path class='cls-1 anim-elem1' d='M100,5C70.6,5,46.8,47.5,46.8,100s23.8,95,53.2,95'/><path class='cls-1' d='M176.6,43.8C159.3,57,131.4,65.6,100,65.6S40.7,57,23.4,43.8'/><path class='cls-1' d='M176.6,156.2c-17.3-13.2-45.2-21.8-76.6-21.8S40.7,143,23.4,156.2'/><line class='cls-1' x1='100' y1='5' x2='100' y2='195'/></svg>
                </a>

                <CloseBtn
                    :glassTile="true"
                    @click="
                        scrollTopModal(),
                        $emit('hideModals')
                    "
                />

            </div>

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
    cursor:var(--cursorDefault);
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

    & .modal-hub{
        position:absolute;
        top:var(--size6);
        right:var(--size6);

        display:flex;
        gap:var(--size4);

        opacity:0;
        transition:all var(--trans2), opacity var(--trans3) !important;
        z-index:1000;

        & .modal-hub-link{
            width:calc(var(--size7) + 4px);
            height:calc(var(--size7) + 4px);
            position:relative;
            
            display:flex;
            cursor:var(--cursorHover);

            &:hover{
                transform:scale(1.2);
            }
   
            &:before{
                content:"";
                width:calc(100% + var(--size2));
                aspect-ratio:1/1;

                position:absolute;
                top:50%;
                left:50%;
                transform:translate(-50%, -50%);

                background-color:var(--colorBg1c);
                border-radius:50%;
                z-index:-1;
            }
       
            &:hover svg{
                animation:navAnimElem 2s ease-in-out infinite;
            }

            &.mh-link1:hover .anim-elem1{
                animation:navAnimElem1 2s ease-in-out infinite;
                transform-origin:100px 144px;
            }

            &.mh-link2:hover :is(.anim-elem1, .anim-elem2){
                animation:projAnimElem2 2s ease-in-out infinite;
                transform-origin:100px 100px;
            }

            & *{
                fill:none;
                stroke-linecap:round;
                stroke-miterlimit:10;

                stroke:#FFF;
                stroke-width:10px;
            }

        }

    }

    @keyframes projAnimElem2{
        0%{
            transform:scaleX(1);
        }
        6%{
            transform:scaleX(1.2);
        }
        14%{
            transform:scaleX(0.85);
        }
        22%{
            transform:scaleX(1.1);
        }
        30%{
            transform:scaleX(1);
        }
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
        padding:var(--size8);
        
        & p{
            text-align:center;
        }

    }

    & .project-desc{
        display:flex;
        flex-wrap:wrap;
        align-items:flex-start;
        gap:var(--size8);

        & .desc-elem{
            padding:var(--size8);
            transition:0s;
        }

        & .desc-elem-inner{
            display:flex;
            flex-direction:column;
            gap:var(--size3);
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
        width:100dvw;
        height:100dvh;

        border-radius:0;
        pointer-events:all;

        &:before{
            border-radius:0;
        }

        & .modal-hub,
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

@media screen and (width <= 440px){

    .tile-section .tile-modal{
 
        & .project-overview{
            padding:var(--size8) var(--size6);
        }

        & .project-desc{

            & .desc-elem{
                padding:var(--size8) var(--size6);
            }

        }

    }

}

</style>