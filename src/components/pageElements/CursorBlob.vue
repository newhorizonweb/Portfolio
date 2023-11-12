


<template>

    <div class="cursor-blob"
        :class="{'cursor-blob-visible': wasCursorMoved}"
        ref="cursorBlob"></div>

</template>



<script lang="ts">
import { defineComponent } from 'vue'

export default defineComponent({
    name: "CursorBlob",

    data(){
        return{

            // Settings
            cursorBlobSize: 48,     // width in px

            // Code
            cursorBlob: null as null | HTMLElement,
            mobilePage: false,
            wasCursorMoved: false,
            halfBlobSize: 0
        }
    },

    mounted(){

        // Cursor Blob
        this.cursorBlob = this.$refs.cursorBlob as HTMLElement;
        this.cursorBlob.style.width = `${this.cursorBlobSize}px`;

        // Set the blob's half-size
        this.halfBlobSize = this.cursorBlobSize / 2;

        // check the page size (mobile/desktop)
        this.checkIfMobile;
        window.addEventListener("resize", this.checkIfMobile);

        // Cursor blob position
        window.addEventListener("mousemove", this.cursorBlobPos);

        // Check if the cursor is outside the page
        document.body.addEventListener("mouseleave", this.outOfBounds);

    },

    methods:{

        checkIfMobile(){

            if (window.innerWidth <= 768){
                this.mobilePage = true;
                this.wasCursorMoved = false;
            } else {
                this.mobilePage = false;
            }

        },

        outOfBounds(){

            this.cursorBlob!.classList.remove("cursor-blob-visible");
            this.wasCursorMoved = false;

        },

        cursorBlobPos(e: MouseEvent){

            if (this.mobilePage) return;

            // Set the blob position
            requestAnimationFrame(() => {
                this.cursorBlob!.style.transform =
                    `translate3d(
                        ${e.clientX - this.halfBlobSize}px, 
                        ${e.clientY - this.halfBlobSize}px, 
                        0px)
                    `;
            });

            // Show the blob
            if (!this.wasCursorMoved){
                this.wasCursorMoved = true;
                this.cursorBlob!.classList.add("cursor-blob-visible");
            }

        }
        
    }

});
</script>



<style lang="scss">

.cursor-blob{
    will-change:transform;
    aspect-ratio:1/1.1;

    position:fixed;
    top:0;
    left:0;
    
    opacity:0;
    border-radius:50%;

    transition:all 0.15s, opacity 1s 0.15s;
    pointer-events:none;
    z-index:999999;

    &.cursor-blob-visible{
        opacity:1;
    }

    &:after{
        content:"";
        width:100%;
        height:100%;

        position:absolute;
        top:0;
        left:0;

        opacity:0.7;
        background:linear-gradient(to right,
            var(--color1a), var(--color1b));
        border-radius:50%;
        filter:blur(30px);

        animation:cursorBlobAnim 6s linear infinite;
    }

}

@keyframes cursorBlobAnim{
    0%{
        transform:rotate(0);
    }
    100%{
        transform:rotate(360deg);
    }
}

@media screen and (width <= 768px){
        
    .cursor-blob{

        &.cursor-blob-visible{
            opacity:0;
        }

    }

}

</style>