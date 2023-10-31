


<template>

    <div id="dev-projects" class="tile-section wrapper main-section"
        :class="{'odd-tiles': !isTileNumberEven}">

        <h2 class="section-heading"
            :data-text="sectionTitle">
        </h2>

        <div class="project-tile glass-tile"
            ref="projectTile"

            v-for="content in contents" 
            :key="content.title">

            <component
                :is="modalComp"
                
                :data="content"
                @hideModals="hideModals"
            />

        </div>

    </div>

</template>



<script lang="ts">
import { defineComponent } from 'vue';

export default defineComponent({
    name: "TilesSection",

    props:[
        "modalComp",
        "contents",
        "sectionTitle"
    ],

    data(){
        return{
            currProjTile: null as null | HTMLElement,
            isTileNumberEven: null as boolean | null,
            tiles: null as null | HTMLElement[]
        } 
    },

    mounted(){

        // Get the tiles
        this.tiles = this.$refs.projectTile as HTMLElement[];

        // Check if the tile number is even
        if (this.contents.length % 2 === 0){
            this.isTileNumberEven = true;
        } else {
            this.isTileNumberEven = false;
        }

        // Add the tile click events
        this.tileModal();

        // Modal placement on resize
        let resizeTimer: number;

        window.addEventListener("resize", () => {

            clearTimeout(resizeTimer);

            if (this.currProjTile &&
            this.currProjTile.classList.contains("tile-modal-open")){

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

        hideModals(currTile?: HTMLElement){

            // Disable the modal mode
            document.documentElement.classList.remove("modal-mode");

            this.tiles?.forEach((tile) => {

                (tile.querySelector(".tile-modal") as HTMLElement)!.style.transform = "translate3d(0px, 0px, 0px)";
                    
                tile.classList.remove("tile-modal-open");
                tile.classList.remove("no-trans");

                if (tile !== currTile){
                    setTimeout(() => {
                        tile.classList.remove("modal-opacity");
                    }, 600);
                }

            });

        },

        currTilePos(tile: HTMLElement){

            // Get the tile position
            const rect = tile.getBoundingClientRect();
            const transX = -rect.left;
            const transY = -rect.top;

            // Set the transform property (position modal in the center)
            (tile.querySelector(".tile-modal") as HTMLElement)!.style.transform = 
                `translate3d(${transX}px, ${transY}px, 0px)`;

        },

            /* Doing Stuff */

        tileModal(){

            this.tiles?.forEach((tile) => {
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
                        tile.classList.add("tile-modal-open");
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

.tile-section{
    display:flex;
    position:relative;
    flex-wrap:wrap;
    gap:var(--size8);

    &:has(.tile-modal-open){
        z-index:11000;

        & .project-tile:not(.tile-modal-open){
            pointer-events:none;
        }

    }

        /* Tile */

    & .project-tile{
        width:calc(50% - (var(--size8) / 2));
        height:300px;
        position:relative;

        box-shadow:inset 0 0 0 0 transparent;
        cursor:pointer;

        &.tile-modal-open{
            z-index:11000;
            cursor:auto;
        }

        &.modal-opacity{
            z-index:50;
        }

        &:hover{
            box-shadow:inset 0 0 max(5vw, 50px) 1px rgba(222, 183, 255, 0.25);
        }

    }

    &.odd-tiles .project-tile:nth-last-of-type(1){
        width:100%; /* If the number of tiles is odd */
    }

    &:has(.modal-opacity) .project-tile:not(.modal-opacity){
        pointer-events:none;
    }

}

@media screen and (width <= 768px){

    .tile-section{

        & .project-tile{
            width:100%;
            height:275px;
        }

    }

}

</style>