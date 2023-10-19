


<template>

    <div id="dev-projects" class="dev-projects wrapper">

        <h2 class="section-heading"
            data-text="Web-Dev Projects">
        </h2>

        <div class="project-tile glass-tile"
            ref="projectTile"

            v-for="project in projects" 
            :key="project.title">

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
    mockupImg: string;
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
                    
                    mobileMockup: this.path('cookbook-mobile.png'),
                    desktopMockup: this.path('cookbook-desktop.png'),
                },

                {
                    title: "Logo Test",
                    logoSrc: this.path('uverit-logo.svg'),

                    mobileMockup: this.path('cookbook-mobile.png'),
                    desktopMockup: this.path('cookbook-desktop.png'),
                },

                {
                    title: "SkillPeak",
                    logoSrc: this.path('uverit-logo.svg'),

                    mobileMockup: this.path('cookbook-mobile.png'),
                    desktopMockup: this.path('cookbook-desktop.png'),
                },

                {
                    title: "Color Palette",
                    logoSrc: this.path('uverit-logo.svg'),

                    mobileMockup: this.path('cookbook-mobile.png'),
                    desktopMockup: this.path('cookbook-desktop.png'),
                },

                {
                    title: "Rapid Core",
                    logoSrc: this.path('rapid-core-logo.svg'),

                    mobileMockup: this.path('cookbook-mobile.png'),
                    desktopMockup: this.path('cookbook-desktop.png'),
                },
            ],

            // Modal
            currProjTile: null as null | HTMLElement

        } 
    },

    mounted(){

        // Add the tile click events
        this.tileModal();

        // Modal placement on resize
        let resizeTimer: number;

        window.addEventListener("resize", () => {

            clearTimeout(resizeTimer);

            if (this.currProjTile &&
            this.currProjTile.classList.contains("tile-modal")){

                this.currTilePos(this.currProjTile);

                // Ensure the correct placement
                // Sometimes the resize event dwould not be registered correctly
                resizeTimer = setTimeout(() => {
                    this.currTilePos(this.currProjTile!);
                }, 400);

            }

        });

    },

    methods:{

            /* Base Function Elements */

        path(imgName: string){
            return require("@/assets/img/" + imgName);
        },

        hideModals(currTile?: HTMLElement){

            // Disable the modal mode
            document.documentElement.classList.remove("modal-mode");

            const tiles = this.$refs.projectTile as HTMLElement[];

            tiles.forEach((tile) => {

                (tile.querySelector(".project-modal") as HTMLElement)!.style.transform = "translate3d(0px, 0px, 0px)";
                    
                tile.classList.remove("tile-modal");
                tile.classList.remove("no-trans");

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

                        // Remove the transition effect after the modal has covered the page
                        setTimeout(() => {
                            tile.classList.add("no-trans");
                        }, 750);

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
   
        cursor:pointer;

        &:nth-last-of-type(1){
            width:100%; /* If the number of tiles is odd */
        }

        &.tile-modal{
            z-index:11000;
        }

        &.modal-opacity{
            z-index:50;
        }

        &:hover{
            box-shadow:inset 0 0 max(5vw, 50px) 1px rgba(222, 183, 255, 0.25);
        }

    }

}

@media screen and (width <= 540px){

    .dev-projects{

        & .project-tile{
            width:100%;
            height:275px;
        }

    }

}

</style>