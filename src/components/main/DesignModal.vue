


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
                    @click="currSrc = design"

                    v-for="(design, index) in data.designs"
                    :key="index">

                    <div class="design-proj-inner"
                        :class="{'dark-modal': bgModalDark}">

                        <div class="toggle-modal-bg"
                            @click="bgModalDark = !bgModalDark">

                            <img :src="require('@/assets/img/sun.svg')" 
                                alt="Toggle Modal Background" class="toggle-modal-img"
                                v-if="!bgModalDark">

                            <img :src="require('@/assets/img/moon.svg')" 
                                alt="Toggle Modal Background" class="toggle-modal-img"
                                v-else>

                        </div>

                        <div class="close-modal"
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

                /* Modal */

            currTile: null as null | HTMLElement,
            tiles: null as null | HTMLElement[],

                /* BG Color */

            imgScaledWidth: 200,
            currSrc: null as null | string,
            bgModalDark: false
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
                    }, 600);
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
            (tile.querySelector(".design-proj-inner") as HTMLElement)!.style.transform = 
                `translate3d(${transX}px, ${transY}px, 0px)`;

        },

            /* Modal Background Color */

        autoBgMode(){

            if (this.currSrc){

                // Create a new image element
                const img:HTMLImageElement = document.createElement("img");
                img.src = this.currSrc;

                img.addEventListener('load', () => {

                    // Image ratio
                    const imgRatio = img.width / img.height;

                    // Image new height
                    const imgScaledHeight = 
                        Math.round(this.imgScaledWidth / imgRatio);
                    
                    // Create a canvas element
                    const canvas:HTMLCanvasElement = document.createElement('canvas');
                    canvas.width = this.imgScaledWidth;
                    canvas.height = imgScaledHeight;

                    // Draw the image on the canvas
                    const ctx:CanvasRenderingContext2D | null = canvas.getContext('2d');
                    ctx!.drawImage(img, 0, 0, canvas.width, canvas.height);

                    // Get the image data
                    const imageData:ImageData = ctx!.getImageData(0, 0, canvas.width, canvas.height);
                    const data:Uint8ClampedArray = imageData.data;

                    // Max and min color values
                    let maxVal = 0;
                    let minVal = 0;

                    // The total number of non-transparent pixels
                    let totAlpha = 0;

                    for (let i = 0; i < data.length; i += 4){
                        const r = data[i];
                        const g = data[i + 1];
                        const b = data[i + 2];
                        const a = data[i + 3];

                        if (a > 0){
                            maxVal += Math.max(r, g, b);
                            minVal += Math.min(r, g, b);
                            totAlpha++
                        }
                    }

                    // Calculate lightness
                    const lightnessSum = (maxVal + minVal) / 2;
                    const lightness = Math.round(lightnessSum / totAlpha / 255 * 100);

                    // Change the bg color
                    if (lightness >= 80){
                        this.bgModalDark = true;
                    } else {
                        this.bgModalDark = false;
                    }

                });

            }

        },

            /* Doing Stuff */

        tileModal(){

            this.tiles?.forEach((tile) => {
                tile.addEventListener("click", (e: Event) => {

                    if (e.target === tile){

                        // Change the modal bg color automatically 
                        // Based on the average image color
                        setTimeout(this.autoBgMode, 0);

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
            width:calc(100% + var(--size6));
            height:calc(100% + var(--size6));
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

        & .close-modal{
            background-color:rgb(255,255,255,0.75);
            border:solid 2px #000;
            border-radius:50%;

            &:before,
            & span{
                background-color:#000;
            }

        }

        & .toggle-modal-bg{
            width:calc(var(--size7) + 4px);
            aspect-ratio:1/1;

            position:absolute;
            top:var(--size6);
            right:calc(
                var(--size7) +
                var(--size6) +
                var(--size4)
            );

            display:flex;
            justify-content:center;
            align-items:center;

            opacity:0;
            background-color:rgb(255,255,255,0.75);
            border:solid 2px #000;
            border-radius:50%;

            transition:var(--trans2);
            cursor:pointer;
            z-index:120;

            &:before{
                background-color:#000;
            }

            &:hover{
                transform:scale(1.2);
            }

            & .toggle-modal-img{
                width:var(--size6);
            }

        }

        &.dark-modal{

            & .toggle-modal-bg,
            & .close-modal{
                background-color:rgb(0,0,0,0.75);
                border-color:#FFF;
            } 

            & .close-modal span{
                background-color:#FFF;
            }

        }

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

        & .toggle-modal-bg,
        & .close-modal{
            opacity:1;
        }

    }
    
    & .design-opacity{
        z-index:50;

        & .design-proj-inner{
            background-color:#FFF;
        }

        & .design-proj-inner.dark-modal{
            background-color:#111;
        }

    }
    
    & .no-trans .design-proj-inner{
        transition:all 0s,
            background var(--trans2);
    }

}

// Hide the Close Button (from the modal with all designs)
.tile-modal-inner:has(.design-open) > .close-modal{
    opacity:0 !important;
    pointer-events:none;
}

</style>