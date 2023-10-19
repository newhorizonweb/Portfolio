


<template>

    <div class="project-display">
        <div class="project-img">
            <img :src="data.logoSrc" :alt="data.title">
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

.tile-modal .project-display{
    height:calc(170px + (var(--size8) * 2)); // border box, so add paddings
    padding:var(--size8) 0;
}

.project-tile:not(.tile-modal):hover .project-display{
    transform:scale(0.8);
    filter:brightness(110%);
}

@media screen and (width <= 768px){

    .project-display{

        & .project-img{
            height:120px;
        }

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