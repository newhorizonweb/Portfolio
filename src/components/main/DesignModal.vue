


<template>

    <div class="tile-modal design-modal"
        :class="data.designClass">

        <div class="tile-modal-inner hide-scrollbar"
            ref="innerModal">

            <TileDisplay
                :data="data"
            />

            <div class="close-modal glass-tile"
                @click="
                    scrollTopModal(),
                    $emit('hideModals')
                ">

                <span></span>
                <span></span>
            </div>

            <div class="modal-content wrapper">

                <div class="design-project glass-tile"
                    ref="designTile"

                    v-for="(design, index) in data.designs"
                    :key="index">

                    <div class="design-proj-inner">

                        <div class="close-modal glass-tile"
                            @click="hideDesignModals">

                            <span></span>
                            <span></span>
                        </div>

                        <img :src="design" alt="Graphic Design Project">

                    </div>
                    
                </div>

            </div>

        </div>

    </div>

</template>



<script lang="ts">
import { defineComponent } from 'vue';
import TileDisplay from "../main/TileDisplay.vue";

export default defineComponent({
    name: "ProjectModal",

    components:{
        TileDisplay
    },

    props:[
        "data"
    ],

    emits:[
        "hideModals"
    ],

    data(){
        return{
            currTile: null as null | HTMLElement,
            tiles: null as null | HTMLElement[]
        } 
    },

    mounted(){

        // Get the tiles
        this.tiles = this.$refs.designTile as HTMLElement[];

        // Add the tile click events
        this.tileModal();

        // Modal placement on resize
        let resizeTimer: number;

        window.addEventListener("resize", () => {

            clearTimeout(resizeTimer);

            if (this.currTile &&
            this.currTile.classList.contains("design-open")){

                this.currTilePos(this.currTile);

                // Ensure the correct placement
                // Sometimes the resize event dwould not be registered correctly
                resizeTimer = setTimeout(() => {
                    this.currTilePos(this.currTile!);
                }, 420);

            }

        });

    },

    methods:{

        scrollTopModal(){

            const innerModal = this.$refs.innerModal as HTMLElement;
            innerModal.scrollTo({
                top:0,
                behavior:"smooth"
            });
            
        },

            /* Base Function Elements */

        hideModals(currTile?: HTMLElement){

            // Disable the modal mode
            document.documentElement.classList.remove("modal-mode");

            this.tiles?.forEach((tile) => {

                (tile.querySelector(".design-proj-inner") as HTMLElement)!.style.transform = "translate3d(0px, 0px, 0px)";
                    
                tile.classList.remove("design-open");
                tile.classList.remove("no-trans");

                if (tile !== currTile){
                    setTimeout(() => {
                        tile.classList.remove("design-opacity");
                    }, 500);
                }

            });

        },

        hideDesignModals(currTile?: HTMLElement){

            this.tiles?.forEach((tile) => {

                (tile.querySelector(".design-proj-inner") as HTMLElement)!.style.transform = "translate3d(0px, 0px, 0px)";
                    
                tile.classList.remove("design-open");
                tile.classList.remove("no-trans");

                if (tile !== currTile){
                    setTimeout(() => {
                        tile.classList.remove("design-opacity");
                    }, 750);
                }

            });

        },

        currTilePos(tile: HTMLElement){

            // Get the tile position
            const rect = tile.getBoundingClientRect();
            const transX = -rect.left;
            const transY = -rect.top;

            // Set the transform property (position modal in the center)
            (tile.querySelector(".design-proj-inner") as HTMLElement)!.style.transform = 
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
                        this.currTile = tile;

                        // Adjust the modal position
                        this.currTilePos(tile);

                        // Show modal
                        tile.classList.add("design-open");
                        tile.classList.add("design-opacity");

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

    /* Layout */

.design-row3{
    --rowDesignNum:3;
}
.design-row4{
    --rowDesignNum:4;
}
.design-row5{
    --rowDesignNum:5;
}

// Square, Horizontal, Vertical
.design-row-s .design-project{
    aspect-ratio:1/1;
}
.design-row-h .design-project{
    aspect-ratio:3/2;
}
.design-row-v .design-project{
    aspect-ratio:2/3;
}

@media screen and (width <= 768px){

    .design-row3{
        --rowDesignNum:2;
    }
    .design-row4{
        --rowDesignNum:3;
    }
    .design-row5{
        --rowDesignNum:4;
    }

}

@media screen and (width <= 540px){

    .design-row5{
        --rowDesignNum:3;
    }

}

@media screen and (width <= 440px){

    .design-row3{
        --rowDesignNum:1;
    }
    .design-row4{
        --rowDesignNum:2;
    }
    .design-row5{
        --rowDesignNum:3;
    }

}

@media screen and (width <= 320px){

    .design-row4{
        --rowDesignNum:1;
    }
    .design-row5{
        --rowDesignNum:2;
    }

}



    /* Tiles & Modals */

.tile-section .design-modal{

    & .tile-modal-inner:has(.design-open){
        overflow:hidden;
    }

    & .modal-content{
        display:grid;
        grid-template-columns:repeat(var(--rowDesignNum), 1fr);
        gap:var(--size6);
    }

    & .design-project{
        width:100%;
        position:relative;
        display:flex;   // Removes jittering on hover

        border-radius:var(--size4);
        backdrop-filter:none;
        cursor:pointer;

        &:before{
            border-radius:inherit;
        }

        &:not(.design-open):hover img{
            transform:scale(1.1);
        }

        & .close-modal{
            opacity:0;
        }

    }

    &:has(.design-opacity) .design-project:not(.design-opacity){
        pointer-events:none;
    }

        /* Design Project Modal */

    & .design-proj-inner{
        width:100%;
        height:100%;
        padding:var(--size6);

        position:absolute;
        top:0;
        left:0;

        display:flex;
        justify-content:center;
        align-items:center;

        border-radius:inherit;
        transition:all 0.75s ease-in-out,
            background-color var(--trans3);

        pointer-events:none;
        overflow:hidden;

        & img{
            width:min(1024px, 100%);
            height:100%;
            object-fit:contain;
            transition:var(--trans3);
        }

    }

        /* Modal Visibility Modes */

    & .design-open{
        z-index:11000;
        cursor:auto;

        & .design-proj-inner{
            width:100vw;
            height:100vh;
            pointer-events:all;
        }

        & .close-modal{
            opacity:1;
        }

    }
    
    & .design-opacity{
        z-index:50;

        & .design-proj-inner{
            background-color:#111;
        }

    }
    
    & .no-trans .design-proj-inner{
        transition:0s;
    }

}

// Hide the Close Button (from the modal with all designs)
.tile-modal-inner:has(.design-open) > .close-modal{
    opacity:0 !important;
    pointer-events:none;
}

</style>