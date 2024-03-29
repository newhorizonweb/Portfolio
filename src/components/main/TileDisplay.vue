


<template>

    <div class="project-display">
        
        <div class="project-img" v-if="!data.imgSrc.includes('</svg>')">
            <img :src="data.imgSrc" :alt="data.title">
        </div>

        <div class="project-img" v-else v-html="data.imgSrc">
     
        </div>

        <h3 class="project-title" :data-text="data.title"></h3>
    </div>

</template>



<script lang="ts">
import { defineComponent } from 'vue';

export default defineComponent({
    name: "TileDisplay",

    props:[
        "data"
    ]

});
</script>



<style lang="scss">

.project-display{
    width:100%;
    height:100%;
    position:relative;

    display:flex;
    flex-direction:column;
    justify-content:center;
    align-items:center;
    gap:var(--size6);

    transition:var(--trans4);

    & .project-img{
        --imgSize:min(220px, 30vw);

        width:var(--imgSize);
        height:calc(var(--imgSize) / 2);

        display:flex;
        justify-content:center;
        align-items:center;

        & :is(img, svg){
            object-fit:contain;
            max-height:100%;
            max-width:100%;
        }

        & svg:not(.tile-svg1, .tile-svg6){
            stroke-linecap:round;
            stroke-linejoin:round;

            fill:none;
            stroke:#FFF;
            stroke-width:8px;
            transition:var(--trans4);

            & .cls-1{
                fill:none;
                stroke-linecap:round;
                stroke-miterlimit:10;
            }

            &.tile-svg5 .anim-elem1{
                fill:var(--colorBg2c);
            }

        }

        & .tile-svg1{

            .cls-1{
                fill:var(--color1a);
            }

            .cls-2{
                fill:#FFF;
            }

        }

        & .tile-svg6{

            & *{
                fill:#FFF;
            }

        }

    }

    & .project-title{
        font-size:min(32px, 4vw);
        text-transform:capitalize;
    }

}

.tile-modal-open .project-display{
    height:calc(170px + (var(--size8) * 2)); // border box, so add paddings
    padding:var(--size8) 0;
}

.project-tile:not(.tile-modal-open):hover .project-display{
    transform:scale(0.8);
    filter:brightness(110%);

    & svg{
        animation:tileSvgAnim 2s ease-in-out infinite;
    }

    & .tile-svg1 .anim-elem1{
        animation:tileSvgAnim1 2s ease-in-out infinite;
    }

    & .tile-svg2{

        & .anim-elem1{
            animation:tileSvgAnim2a 2s ease-in-out infinite;
            transform-origin:center;
        }

        & .anim-elem2a *{
            animation:tileSvgAnim2b1 2s ease-in-out infinite;
        }

        & .anim-elem2b *{
            animation:tileSvgAnim2b2 2s ease-in-out infinite;
        }

        & .anim-elem2 *{
            fill:var(--colorBg2c);
        }

    }

    & .tile-svg3{

        & .anim-elem1{
            animation:tileSvgAnim3a1 2s ease-in-out infinite;
            transform-origin:center;
        }
        & .anim-elem3{
            animation:tileSvgAnim3a2 2s ease-in-out infinite;
            transform-origin:center;
        }

        & .anim-elem2{
            animation:tileSvgAnim3b 2s ease-in-out infinite;
            transform-origin:100px 79px;
        }

        & .anim-elem4{
            animation:tileSvgAnim3c 2s ease-in-out infinite;
            transform-origin:70px 138.6px;
        }

    }

    & .tile-svg4 *{
        animation:tileSvgAnim4 2s ease-in-out infinite;
        transform-origin:center;
    }

    & .tile-svg5 .anim-elem1{
        animation:tileSvgAnim5 2s ease-in-out infinite;
        transform-origin:bottom right;
    }

    & .tile-svg6 .anim-elem1{
        animation:tileSvgAnim6 2s ease-in-out infinite;
    }

}



    /* Animations */

@keyframes tileSvgAnim{
    0%{
        transform:rotate(0deg);
    }
    6%{
        transform:rotate(-15deg);
    }
    14%{
        transform:rotate(10deg);
    }
    22%{
        transform:rotate(-5deg);
    }
    30%{
        transform:rotate(0deg);
    }
}

        /* Tile 1 */

@keyframes tileSvgAnim1{
    0%{
        transform:translate(0, 0);
    }
    6%{
        transform:translate(0, -60px);
    }
    14%{
        transform:translate(0, 35px);
    }
    22%{
        transform:translate(0, -10px);
    }
    30%{
        transform:translate(0, 0);
    }
}

        /* Tile 2 */

@keyframes tileSvgAnim2a{
    0%{
        transform:rotate(0deg);
    }
    30%{
        transform:rotate(180deg);
    }
    100%{
        transform:rotate(180deg);
    }
}
            
@keyframes tileSvgAnim2b1{
    0%{
        transform:translate(0, 0);
    }
    15%{
        transform:translate(-8px, -8px);
    }
    30%{
        transform:translate(0, 0);
    }
}

@keyframes tileSvgAnim2b2{
    0%{
        transform:translate(0, 0);
    }
    15%{
        transform:translate(8px, 8px);
    }
    30%{
        transform:translate(0, 0);
    }
}

        /* Tile 3 */

@keyframes tileSvgAnim3a1{
    0%{
        transform:translate(0, 0);
    }
    10%{
        transform:translate(0, -16px);
    }
    20%{
        transform:translate(0, -16px);
    }
    30%{
        transform:translate(0, 0);
    }
}

@keyframes tileSvgAnim3a2{
    0%{
        transform:translate(0, 0);
    }
    10%{
        transform:translate(0, 16px);
    }
    20%{
        transform:translate(0, 16px);
    }
    30%{
        transform:translate(0, 0);
    }
}

@keyframes tileSvgAnim3b{
    0%{
        transform:rotate(0);
    }
    12%{
        transform:rotate(12deg);
    }
    22%{
        transform:rotate(-9deg);
    }
    25%{
        transform:rotate(3deg);
    }
    30%{
        transform:rotate(0);
    }
}

@keyframes tileSvgAnim3c{
    0%{
        transform:scaleX(1);
    }
    10%{
        transform:scaleX(1.95);
    }
    30%{
        transform:scaleX(1);
    }
}

        /* Tile 4 */

@keyframes tileSvgAnim4{
    0%{
        transform:scale(1);
    }
    15%{
        transform:scale(0.9, 1.1);
    }
    30%{
        transform:scale(1);
    }
}

        /* Tile 5 */

@keyframes tileSvgAnim5{
    0%{
        transform:rotate(0deg);
    }
    8%{
        transform:rotate(-15deg);
    }
    15%{
        transform:rotate(10deg);
    }
    22%{
        transform:rotate(-5deg);
    }
    30%{
        transform:rotate(0deg);
    }
}

        /* Tile 6 */

@keyframes tileSvgAnim6{
    0%{
        opacity:1;
    }
    8%{
        opacity:0;
    }
    15%{
        opacity:1;
    }
    22%{
        opacity:0;
    }
    30%{
        opacity:1;
    }
}



    /* Media */

@media screen and (width <= 768px){

    .project-display{

        & .project-img{
            height:120px;
        }

    }

    .tile-modal-open .project-display{
        height:calc(
            170px +
            var(--size8) +
            (var(--size8) + var(--size7))
        ); // border box, so add paddings

        padding-top:calc(var(--size8) + var(--size7));
    }

}

@media screen and (width <= 540px){

    .project-display{

        & .project-img{
            --imgSize:220px;
        }

        & .project-title{
            font-size:min(32px, 8vw);
        }

    }

}

@media screen and (width <= 440px){

    .project-display{

        & .project-img{
            --imgSize:50vw;
        }

    }

}

</style>