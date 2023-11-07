


<template>

    <div class="tile-modal design-modal"
        :class="data.designClass">

        <div class="tile-modal-inner hide-scrollbar"
            ref="innerModal">

            <TileDisplay
                :data="data"
            />

            <div class="modal-hub">

                <div class="modal-scroll-top glass-tile"
                    :class="{'show-scroll-btn': showModalScrollbtn}"
                    ref="modalScrollTop"
                    @click="modalToTop">

                    <svg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 200 200'><path class='cls-1' d='M33.6,155.6a14.7,14.7,0,0,1-20.7,0l-.5-.6a14.7,14.7,0,0,1,0-20.7L89.6,57.1a14.7,14.7,0,0,1,20.7,0h.1l77.2,77.2a14.7,14.7,0,0,1,0,20.7l-.5.6a14.7,14.7,0,0,1-20.7,0l-66-66a.5.5,0,0,0-.8,0Z'/></svg>
                </div>

                <CloseBtn
                    :glassTile="true"
                    @click="
                        scrollTopModal(),
                        $emit('hideModals')
                    "
                />

            </div>

            <div class="modal-content wrapper">

                <div class="design-project"
                    ref="designTile"
                    @click.self="tileModal"

                    v-for="(design, index) in data.designs"
                    :key="index">

                    <div class="design-proj-inner">

                        <div class="modal-hub">
                            <div class="toggle-modal-bg" @click="toggleModalBg"></div>

                            <CloseBtn
                                :glassTile="false"
                                @click="hideDesignModals"
                            />
                        </div>

                        <img class="design-proj-img" 
                            ref="designProjImg"
                            :src="placeholderImg"
                            :data-src="design" alt="Design Project">

                    </div>
                    
                </div>

            </div>

        </div>

    </div>

</template>



<script lang="ts">
import { defineComponent } from 'vue';
import CloseBtn from "../pageElements/CloseBtn.vue";
import TileDisplay from "../main/TileDisplay.vue";

export default defineComponent({
    name: "ProjectModal",

    components:{
        CloseBtn,
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

            // Elements
            innerModal: null as null | HTMLElement,
            currTile: null as null | HTMLElement,
            tiles: null as null | HTMLElement[],
            
            // Scroll
            scrollOffset: window.innerHeight / 2, // Show the btn if scrolled this amount
            showModalScrollbtn: false,

                /* BG Color */

            // Settings
            imgLoadInterval: 12, // Load this number images each second
            imgScaledWidth: 100,

            // Elements
            canvas: null as HTMLCanvasElement | null,
            ctx: null as CanvasRenderingContext2D | null,
            placeholderImg:require("@/assets/img/placeholder-img.svg")
            
        } 
    },

    mounted(){

        // Elements
        this.innerModal = this.$refs.innerModal as HTMLElement;

        // Modal project image canvas
        this.canvas = document.createElement('canvas');
        this.ctx = this.canvas.getContext('2d', { willReadFrequently: true });

        // Get the tiles
        this.tiles = this.$refs.designTile as HTMLElement[];

        // Load the project design images &&
        // Set the modal auto background color
        const images = this.$refs.designProjImg;
        this.throttleImageLoading(images as HTMLImageElement[]);

        // Modal placement on resize
        let resizeTimer: number;

        window.addEventListener("resize", () => {

            // Set a new scroll offset
            this.scrollOffset = window.innerHeight / 2;

                /* Modal */

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

        // Hide / show the modal scroll btn (if the modal was scrolled or not)
        this.innerModal.addEventListener("scroll", this.modalScrollBtnVisibility);

    },

    methods:{

            /* Modal Scroll */

        modalScrollBtnVisibility(){

            if (this.innerModal!.scrollTop > this.scrollOffset){
                this.showModalScrollbtn = true;
            } else {
                this.showModalScrollbtn = false;
            }

        },

        scrollTopModal(){
            this.innerModal!.scrollTo({
                top:0
            });
        },

        modalToTop(){
            this.innerModal!.scrollTo({
                top:0,
                behavior:"smooth"
            });
        },

            /* Modal Behavior */

        hideDesignModals(currTile?: HTMLElement){

            this.tiles?.forEach((tile) => {

                (tile.querySelector(".design-proj-inner") as HTMLElement)!.style.transform = "translate3d(0px, 0px, 0px)";
                    
                tile.classList.remove("design-open", "no-trans");

                if (tile !== currTile){
                    setTimeout(() => {
                        tile.classList.remove("design-opacity");
                    }, 600);
                }

            });

        },

        hideModals(currTile: HTMLElement){

            // Disable the modal mode
            document.documentElement.classList.remove("modal-mode");

            // Hide the tile modals
            this.hideDesignModals(currTile);

        },

        currTilePos(tile: HTMLElement){

            // Get the tile position
            const rect = tile.getBoundingClientRect();
            const transX = -rect.left;
            const transY = -rect.top;

            // Set the transform property (position modal in the center)
            (tile.querySelector(".design-proj-inner") as HTMLElement)!.style.transform = 
                `translate3d(${transX - 1}px, ${transY}px, 0px)`;

        },

        tileModal(e: Event){

            const tile = 
                (e.target as HTMLElement).closest('.design-project') as HTMLElement;

            // Hide the other modals
            this.hideModals(tile);

            // Set the page to the modal mode
            document.documentElement.classList.add("modal-mode");

            // Set the current modal tile
            this.currTile = tile;

            // Adjust the modal position
            this.currTilePos(tile);

            // Show modal
            tile.classList.add("design-open", "design-opacity");

            // Remove the transition effect after the modal has covered the page
            setTimeout(() => {
                tile.classList.add("no-trans");
            }, 750);

        },

            /* Modal Background Color & Images */

        autoBgMode(tileImg: HTMLImageElement){

            const tile = tileImg.closest(".design-project") as HTMLImageElement;
            const canvas = this.canvas;
            const ctx = this.ctx;

            // Create a new image element
            const img:HTMLImageElement = new Image();
            img.src = tileImg.src;

            img.addEventListener('load', () => {
                if (canvas && ctx){

                    // Image ratio
                    const imgRatio = img.width / img.height;

                    // Image new height
                    const imgScaledHeight = 
                        Math.round(this.imgScaledWidth / imgRatio);
                    
                    // Create a canvas element
                    canvas.width = this.imgScaledWidth;
                    canvas.height = imgScaledHeight;

                    // Draw the image on the canvas
                    ctx.drawImage(img, 0, 0, canvas.width, canvas.height);

                    // Get the image data
                    const imageData:ImageData = ctx.getImageData(0, 0, canvas.width, canvas.height);
                    const data:Uint8ClampedArray = imageData.data;

                    // Max and min color values
                    let maxVal = 0, minVal = 0, totAlpha = 0;

                    for (let i = 0; i < data.length; i += 4){
                        const a = data[i + 3];

                        if (a > 0){
                            const   r = data[i], 
                                    g = data[i + 1], 
                                    b = data[i + 2];

                            maxVal += Math.max(r, g, b);
                            minVal += Math.min(r, g, b);
                            
                            totAlpha++;
                        }
                    }

                    // Calculate lightness
                    const lightnessSum = (maxVal + minVal) / 2;
                    const lightness = Math.round(lightnessSum / totAlpha / 255 * 100);

                    // Change the bg color
                    if (lightness >= 65){
                        tile.classList.add("dark-modal");
                    } else {
                        tile.classList.remove("dark-modal");
                    }

                }
            });

        },

        throttleImageLoading(images: HTMLImageElement[]){

            let currentIndex = 0;

            const loadNextImage = () => {
                if (currentIndex < images.length){

                    const image = images[currentIndex];
                    const imgTile = image.closest(".design-project");
                    const dataSrc = image.getAttribute('data-src');
                    
                    if (imgTile && dataSrc !== null){

                        // Remove the placeholder animation
                        imgTile.classList.add("no-ph-anim");

                        // Replace the placeholder image
                        image.src = dataSrc;

                        image.addEventListener('load', () => {

                            // Set the tile auto bg color
                            this.autoBgMode(image);

                            // Next image
                            currentIndex++;
                            setTimeout(loadNextImage, 1000 / this.imgLoadInterval);

                        });
                    }

                }
            };

            setTimeout(loadNextImage, 500);

        },

        toggleModalBg(e: Event){
            (e.target as HTMLElement)!.closest(".design-project")!.classList.toggle("dark-modal");
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

    & .modal-scroll-top{
        width:calc(var(--size7) + 4px);
        aspect-ratio:1/1;
        position:relative;

        display:flex;
        justify-content:center;
        align-items:center;

        opacity:0;
        border-radius:50%;
        transition:all var(--trans2), opacity var(--trans3) !important;

        overflow:hidden;
        cursor:pointer;
        z-index:120;

        &.show-scroll-btn{
            opacity:1;
        }

        & svg{
            width:60%;
            aspect-ratio:1/1;

            position:relative;
            top:-1px;

            & *{
                stroke-linecap:round;
                stroke-miterlimit:10;

                fill:none;
                stroke:#FFF;
                stroke-width:14px;
            }

        }

        &:hover{
            transform:scale(1.2);

            &:before{
                background:var(--borderGrad2);
            }

            & svg{
                animation:modalScrollTop 4s ease-in-out infinite;
            }

        }

        @keyframes modalScrollTop{
                0%{
                    transform:translate(0, -1px);
                }
                10%{
                    transform:translate(0, 10px);
                }
                17%{
                    transform:translate(0, -100px);
                }
                20%{
                    transform:translate(0, -100px);
                }
                21%{
                    transform:translate(0, 100px);
                }
                50%{
                    transform:translate(0, -1px);
                }
        }

    }

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
        cursor:pointer;

        &:before{
            border-radius:inherit;
        }

        &:after{
            --silverColor:rgb(240,245,255,0.8);

            content:"";
            width:100%;
            height:100%;

            position:absolute;
            top:0;
            left:0;

            background:linear-gradient(105deg, 
                transparent 30%,
                var(--silverColor) 60%,
                transparent 75%,
            );
            background-size:200% 100%;
            background-position:200% 0;

            border-radius:var(--size4);
            animation:shinePlaceholder 4s linear infinite;
        }

        &.no-ph-anim:after{
            display:none;
        }

        &:not(.design-open):hover img{
            width:calc(100% + var(--size6));
            height:calc(100% + var(--size6));
        }

        @keyframes shinePlaceholder{
            0%{
                background-position:200% 0;
            }
            100%{
                background-position:-200% 0;
            }
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

        background-color:#FFF;
        border-radius:inherit;
        transition:all 0.75s ease-in-out,
            background-color var(--trans3);

        pointer-events:none;
        overflow:hidden;

        & .modal-hub{
            opacity:0;
        }

        & .close-btn{
            background-color:rgb(255,255,255,0.75);
            border:solid 2px #000;

            &:before,
            & span{
                background-color:#000;
            }

        }

        & .toggle-modal-bg{
            width:calc(var(--size7) + 4px);
            aspect-ratio:1/1;

            display:flex;
            justify-content:center;
            align-items:center;

            background-color:rgb(255,255,255,0.75);
            border:solid 2px #000;
            border-radius:50%;

            background-image:url("~@/assets/img/sun.svg");
            background-size:var(--size6);
            background-position:center;
            background-repeat:no-repeat;

            transition:var(--trans2);
            cursor:pointer;

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

        & img{
            width:min(1024px, 100%);
            height:100%;
            position:relative;

            object-fit:contain;
            transition:var(--trans3);
        }

    }

    & .dark-modal .design-proj-inner{
        background-color:#111 !important;

        & .toggle-modal-bg,
        & .close-btn{
            background-color:rgb(0,0,0,0.75);
            border-color:#FFF;
        }

        & .toggle-modal-bg{
            background-image:url("~@/assets/img/moon.svg");
        } 

        & .close-btn span{
            background-color:#FFF;
        }

    }

        /* Modal Visibility Modes */

    & .design-open{
        z-index:11000;
        cursor:auto;

        & .design-proj-inner{
            width:100dvw;
            height:100dvh;
            pointer-events:all;
        }

        & .modal-hub{
            opacity:1;
        }

    }
    
    & .design-opacity{
        z-index:50;
    }
    
    & .no-trans .design-proj-inner{
        transition:all 0s,
            background var(--trans2);
    }

}

// Hide the Close Button (from the modal with all designs)
.tile-modal-inner:has(.design-open) > .modal-hub{
    opacity:0 !important;
    pointer-events:none;
}

</style>