


<template>

    <div id="dev-projects" class="dev-projects wrapper">

        <h2 class="section-heading"
            data-text="Web-Dev Projects">
        </h2>

        <div class="project-tile glass-tile"
            v-for="project in projects" 
            :key="project.id" 
            @click="openProjectModal(project)">
            
            <div class="project-tile-inner">
                <div class="project-img">
                    <img :src="project.logoSrc" :alt="project.title">
                </div>

                <h3 class="project-title" :data-text="project.title"></h3>
            </div>

        </div>

    </div>

    <ProjectModal
        v-if="showProjectModal" 
        :data="activeData"
        @closeModal="closeModal"
    />

</template>



<script lang="ts">
import { defineComponent } from 'vue';
import ProjectModal from "./ProjectModal.vue";

interface Project{
  id: number;
  logo: string;
  title: string;
  data: string;
}

export default defineComponent({
    name: "ProjectsSection",

    components: {
        ProjectModal
    },

    data(){
        return{

            projects:[
                // Project Data
                {
                    id: 1,
                    title: "Cookbook",
                    logoSrc: this.path('uverit-logo.svg'),
                    
                    data: "aaa1",
                },

                {
                    id: 2,
                    title: "Logo Test",
                    logoSrc: this.path('uverit-logo.svg'),

                    data: "bbb2",
                },

                {
                    id: 3,
                    title: "SkillPeak",
                    logoSrc: this.path('uverit-logo.svg'),

                    data: "bbb2",
                },

                {
                    id: 4,
                    title: "Color Palette",
                    logoSrc: this.path('uverit-logo.svg'),

                    data: "bbb2",
                },

                {
                    id: 5,
                    title: "Rapid Core",
                    logoSrc: this.path('rapid-core-logo.svg'),

                    data: "bbb2",
                },

            ],

            // Modal
            showProjectModal: false,
            activeData: null as Project | null,

        } 
    },

    methods:{

        path(logoName: string){
            return require("@/assets/img/" + logoName);
        },

        openProjectModal(project: Project){
            this.activeData = project;
            this.showProjectModal = true;
        },

        closeModal(){
            this.showProjectModal = false;
        }

    }

});
</script>



<style lang="scss">

.dev-projects{
    padding-top:calc(var(--size8) * 2.5);
    display:flex;
    flex-wrap:wrap;
    gap:var(--size8);

    & .project-tile{
        flex:40%;
        height:300px;
        box-shadow:inset 0 0 0 0 transparent;

        transition:0.25s cubic-bezier(.59,.09,.86,.66);
        overflow:hidden;
        cursor:pointer;

        &:hover{
            transform:scale(1.025);
            box-shadow:inset 0 0 max(5vw, 50px) 1px rgba(222, 183, 255, 0.25);
        }

        & .project-tile-inner{
            width:100%;
            height:100%;
            position:relative;
            perspective: 1500px;

            display:flex;
            flex-direction:column;
            justify-content:center;
            align-items:center;
            gap:var(--size6);

            transition:0.25s cubic-bezier(.59,.09,.86,.66);
            transition-delay:0.15s;
        }

        &:not(:hover) .project-tile-inner{
            animation:tileZoomRev 0.25s cubic-bezier(.59,.09,.86,.66);
        }

        &:hover .project-tile-inner{
            transform:scale(0.85);
            filter:brightness(110%);
            animation:tileZoomInit 0.25s 0.15s cubic-bezier(.59,.09,.86,.66),
                tileZoom 3s 1s ease-in-out infinite;
        }

        & .project-img{
            --imgSize:min(220px, 30vw);

            width:var(--imgSize);
            height:calc(var(--imgSize) / 2);

            display:flex;
            justify-content:center;
            align-items:center;

            & img{
                object-fit:contain;
                max-height:100%;
                max-width:100%;
            }

        }

        & .project-title{
            font-size:min(32px, 4vw);
            text-transform:capitalize;
        }

    }

}

@keyframes tileZoomInit{
    0%{
        transform:scale(1);
    }
    100%{
        transform:scale(0.85);
    }
}

@keyframes tileZoomRev{
    0%{
        transform:scale(0.85);
    }
    100%{
        transform:scale(1);
    }
}

@keyframes tileZoom{
    0%{
        transform:scale(0.85);
    }
    50%{
        transform:scale(0.9);
    }
    100%{
        transform:scale(0.85);
    }
}

@media screen and (width <= 768px){

    .dev-projects{

        & .project-tile{

            & .project-img{
                height:120px;
            }

        }

    }

}

@media screen and (width <= 540px){

    .dev-projects{

        & .project-tile{
            flex:100%;
            height:275px;

            & .project-img{
                --imgSize:220px;
            }

            & .project-title{
                font-size:min(32px, 8vw);
            }

        }

    }

}

@media screen and (width <= 440px){

    .dev-projects{

        & .project-tile{

            & .project-img{
                --imgSize:50vw;
            }

        }

    }

}

</style>