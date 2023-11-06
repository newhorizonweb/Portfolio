


<template>

    <div class="close-btn"
        :class="{
            'glass-tile': glassTile,
            'standard-btn': !glassTile,
        }">

        <span></span>
        <span></span>
        
    </div>

</template>



<script lang="ts">
import { defineComponent } from 'vue'

export default defineComponent({
    name: "CloseBtn",

    props:[
        "glassTile"
    ]
});
</script>



<style lang="scss">

.close-btn{
    width:calc(var(--size7) + 4px);
    aspect-ratio:1/1;
    position:relative;
    border-radius:50%;

    transition:all var(--trans2), opacity var(--trans3) !important;
    cursor:pointer;
    z-index:120;

    &.glass-tile:hover:before{
        background:var(--borderGrad2);
    }

    &.standard-btn{
        border:solid 2px #FFF;
    }

    &:before{
        background-color:#FFF;
    }

    &:hover{
        transform:rotate(90deg) scale(1.2);
    }

    & span{
        width:var(--size5);
        height:2px;

        position:absolute;
        top:50%;
        left:50%;
        transform:translate(-50%, -50%) rotate(45deg);

        background-color:#FFF;
        border-radius:200px;
        transition:var(--trans2);
    }

    & span:nth-of-type(2){
        transform:translate(-50%, -50%) rotate(-45deg);
    }

}

</style>