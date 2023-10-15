


<template>

    <div id="dev-projects" class="dev-projects wrapper">

        <h2 class="section-heading"
            data-text="Web-Dev Projects">
        </h2>

        <div class="project-tile glass-tile"
            ref="projectTile"

            v-for="project in projects" 
            :key="project.title">
            
            <div class="pt-display">
                <div class="project-img">
                    <img :src="project.logoSrc" :alt="project.title">
                </div>

                <h3 class="project-title" :data-text="project.title"></h3>
            </div>

            <ProjectModal
                :data="project"

                @hideModals="hideModals"
            />

        </div>

    </div>

</template>



<script lang="ts">
import { defineComponent } from 'vue';
import ProjectModal from "./ProjectModal.vue";

interface Project{
    logo: string;
    title: string;
    data: string;
}

export default defineComponent({
    name: "ProjectsSection",

    components:{
        ProjectModal
    },

    data(){
        return{

            // Project Data
            projects:[
                {
                    title: "Cookbook",
                    logoSrc: this.path('uverit-logo.svg'),
                    
                    data: "aaa1",
                },

                {
                    title: "Logo Test",
                    logoSrc: this.path('uverit-logo.svg'),

                    data: "bbb2",
                },

                {
                    title: "SkillPeak",
                    logoSrc: this.path('uverit-logo.svg'),

                    data: "bbb2",
                },

                {
                    title: "Color Palette",
                    logoSrc: this.path('uverit-logo.svg'),

                    data: "bbb2",
                },

                {
                    title: "Rapid Core",
                    logoSrc: this.path('rapid-core-logo.svg'),

                    data: "bbb2",
                },
            ],

            // Modal
            currProjTile: null as null | HTMLElement

        } 
    },

    mounted(){

        // Add the tile click events
        this.tileModal();

        window.addEventListener("resize", () => {

            if (this.currProjTile){
                this.currTilePos(this.currProjTile);
            }

        });

    },

    methods:{

            /* Base Function Elements */

        path(logoName: string){
            return require("@/assets/img/" + logoName);
        },

        hideModals(currTile?: HTMLElement){

            // Disable the modal mode
            document.documentElement.classList.remove("modal-mode");

            const tiles = this.$refs.projectTile as HTMLElement[];

            tiles.forEach((tile) => {

                (tile.querySelector(".project-modal") as HTMLElement)!.style.transform = 
                    "translate3d(0px, 0px, 0px)";
                tile.classList.remove("tile-modal");

                if (tile !== currTile){
                    setTimeout(() => {
                        tile.classList.remove("modal-opacity");
                    }, 500);
                }

            });

        },

        currTilePos(tile: HTMLElement){

            // Get the tile position
            const rect = tile.getBoundingClientRect();
            const transX = -rect.left;
            const transY = -rect.top;

            // Set the transform property (position modal in the center)
            (tile.querySelector(".project-modal") as HTMLElement)!.style.transform = 
                `translate3d(${transX}px, ${transY}px, 0px)`;

        },

            /* Doing Stuff */

        tileModal(){

            const tiles = this.$refs.projectTile as HTMLElement[];

            tiles.forEach((tile) => {
                tile.addEventListener("click", (e: Event) => {

                    if (e.target === tile){

                        // Hide the other modals
                        this.hideModals(tile);

                        // Set the page to the modal mode
                        document.documentElement.classList.add("modal-mode");

                        // Set the current modal tile
                        this.currProjTile = tile;

                        // Adjust the modal position
                        this.currTilePos(tile);

                        // Show modal
                        tile.classList.add("tile-modal");
                        tile.classList.add("modal-opacity");

                    }

                });
            });

        }

    }

});
</script>



<style lang="scss">

.modal-mode{
    overflow:hidden;
}

.dev-projects{
    display:flex;
    position:relative;
    flex-wrap:wrap;
    gap:var(--size8);

    &:has(.tile-modal){
        z-index:11000;
    }

        /* Tile */

    & .project-tile{
        width:calc(50% - (var(--size8) / 2));
        height:300px;
        position:relative;

        box-shadow:inset 0 0 0 0 transparent;
        transition:var(--trans3);
        cursor:pointer;

        &:nth-last-of-type(1){
            width:100%; /* If the number of tiles is odd */
        }

        &.tile-modal{
            z-index:11000;
        }

        &:hover{
            box-shadow:inset 0 0 max(5vw, 50px) 1px rgba(222, 183, 255, 0.25);
        }

        & .pt-display{
            width:100%;
            height:100%;
            position:relative;

            display:flex;
            flex-direction:column;
            justify-content:center;
            align-items:center;
            gap:var(--size6);

            transition:var(--trans3);
            pointer-events:none;
        }

        &:not(.tile-modal):hover .pt-display{
            transform:scale(0.8);
            filter:brightness(110%);
        }

        &.tile-modal .pt-display{
            transform:scale(0.8);
            filter:brightness(110%);
            animation:tileZoom 3s ease-in-out infinite;
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

@keyframes tileZoom{
    0%{
        transform:scale(0.8);
    }
    50%{
        transform:scale(1);
    }
    100%{
        transform:scale(0.8);
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
            width:100%;
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