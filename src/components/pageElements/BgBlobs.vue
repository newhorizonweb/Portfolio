


<template>

    <div class="bg-blobs" ref="bgBlobs"></div>

</template>

<script lang="ts">
import { defineComponent } from 'vue'

type BlobData = {
    element: HTMLDivElement;
    position: {
        x: number;
        y: number;
    };
    speed: {
        x: number;
        y: number;
    };
};

export default defineComponent({
    name: "BgBlobs",

    data(){
        return{
            // Blob Settings
            speedFactor: 2, // from 0 (no movement) | 10+ is really fast
            blobSizeMin: 30,
            blobSizeMax: 150,
            blobFPS: 4, // changed based on the screen width

            // Blob Code
            blobSpeed: 0,
            blobs: [] as BlobData[],
            blobNumber: this.calculateBlobNumber(),

            // Elements
            blobContainer: null as null | HTMLElement
        }
    },

    mounted(){

        // Elements
        this.blobContainer = this.$refs.bgBlobs as HTMLElement;

        // Functions
        this.createBlob();
        this.animateBlobs();

        // Event Listeners
        window.addEventListener('resize', this.handleResize);

        // Variables / Code
        this.blobSpeed = (1000 / this.blobFPS) / 100 * this.speedFactor;

    },

    beforeUnmount(){
        window.removeEventListener('resize', this.handleResize);
    },

    methods:{

        createBlob(){

            for (let i = 0; i < this.blobNumber; i++){

                // Create the blob element
                const blob = document.createElement("div");
                blob.classList.add("bg-blob");

                // Random Size
                const size = Math.round(
                    Math.random() * (this.blobSizeMax - this.blobSizeMin) + this.blobSizeMin
                );
                blob.style.width = size + "px";
                blob.style.height = size + "px";

                // Random Position & Speed
                const posX = Math.floor(Math.random() * 
                    (this.blobContainer!.offsetWidth - size + 1));
                const posY = Math.floor(Math.random() * 
                    (this.blobContainer!.offsetHeight - size + 1));

                const blobData = {
                    element: blob,
                    position:{ 
                        x: posX,
                        y: posY
                    },
                    speed:{
                        x: (Math.random() * 2 - 1),
                        y: (Math.random() * 2 - 1)
                    }
                };

                // Append the blob and set its position
                this.blobs.push(blobData);
                blob.style.transform = `translate3d(${posX}px, ${posY}px, 0px)`;
                this.blobContainer!.appendChild(blob);

            }

        },

        animateBlobs(){

            const blobContW = this.blobContainer!.offsetWidth;
            const blobContH = this.blobContainer!.offsetHeight;

            const updateBlobs = () => {

                // Adjust the position
                for (let blobData of this.blobs){

                    const blob = blobData.element;

                    // Blob Speed
                    const blobSpeedX = blobData.speed.x;
                    const blobSpeedY = blobData.speed.y;

                    // Update position based on velocity and delta-time
                    blobData.position.x += blobSpeedX * this.blobSpeed;
                    blobData.position.y += blobSpeedY * this.blobSpeed;

                    // Blob Position
                    const blobPosX = blobData.position.x;
                    const blobPosY = blobData.position.y;

                    // Bounce the blob off the screen edge
                    if (blobPosX < 0 || 
                        blobPosX + blob.offsetWidth > blobContW){

                        blobData.speed.x = -blobSpeedX;
                    }

                    if (blobPosY < 0 ||
                        blobPosY + blob.offsetHeight > blobContH){

                        blobData.speed.y = -blobSpeedY;
                    }

                    // Set blob's new position
                    blob.style.transform = 
                        `translate3d(${blobData.position.x}px, 
                        ${blobData.position.y}px, 
                        0px)`;
                }

                // Next Frame
                setTimeout(updateBlobs, 1000 / this.blobFPS);

            };

            // Start the animation loop
            updateBlobs();

        },

        calculateBlobNumber(){
            const width = window.innerWidth;
            let newBlobNumber = 10;

            switch (true){
                case width <= 768:
                    newBlobNumber = 6;
                    break;

                case width <= 1024:
                    newBlobNumber = 7;
                    break;

                case width <= 1440:
                    newBlobNumber = 8;
                    break;

                default:
                    newBlobNumber = 10;
            }

            return newBlobNumber;
        },

        adjustBlobsPosition(){

            const blobContW = this.blobContainer!.offsetWidth;
            const blobContH = this.blobContainer!.offsetHeight;

            this.blobs.forEach(blobData => {

                const blob = blobData.element;

                // Check if the blob's x position goes out of the right boundary
                if (blobData.position.x + blob.offsetWidth > blobContW){

                    blobData.position.x = 
                        this.blobContainer!.offsetWidth - blob.offsetWidth;
                }

                // Check if the blob's y position goes out of the bottom boundary
                if (blobData.position.y + blob.offsetHeight > blobContH){
                    
                    blobData.position.y = 
                        this.blobContainer!.offsetHeight - blob.offsetHeight;
                }

                // Update the blob's transform to reflect any position adjustments
                blob.style.transform = 
                    `translate3D(${blobData.position.x}px,
                     ${blobData.position.y}px, 
                     0px)`;

            });

        },

        handleResize(){

            // Change the blob position (if they go out of the view)
            this.adjustBlobsPosition();

            // New blob number (based on the screen width)
            const newBlobNumber = this.calculateBlobNumber();

            // Return if the blob count is the same as before
            if (this.blobNumber === newBlobNumber) return;

            if (newBlobNumber > this.blobNumber){
                // Create the needed difference in blob count
                this.blobNumber = newBlobNumber - this.blobNumber;
                this.createBlob();
            } else {
                // Remove the excess
                const difference = this.blobNumber - newBlobNumber;

                // Remove from DOM
                for (let i = 0; i < difference; i++){
                    const blobData = this.blobs.pop();
                    
                    if (blobData){
                        this.blobContainer!.removeChild(blobData.element);
                    }
                }
            }

            // Update the blob number
            this.blobNumber = newBlobNumber;

        }

    }
    
});
</script>



<style lang="scss">
.bg-blobs{
    width:100vw;
    height:100vh;

    position:fixed;
    top:0;
    left:0;
    overflow:hidden;

    .bg-blob{
        will-change:transform;
        position:absolute;
        border-radius:50%;

        transition:transform 0.4s linear;
        overflow:hidden;
        z-index:10;
        
        &:after{
            content:"";
            width:100%;
            height:105%;
            position:absolute;

            background:linear-gradient(to right,
                var(--color2a), var(--color2b));
            border-radius:50%;
            filter:blur(32px);
            transition:var(--trans3);
        }

        &:nth-of-type(2n + 1):after{
            content:"";
            width:100%;
            height:105%;
            position:absolute;

            background:linear-gradient(to right,
                var(--color3a), var(--color3b));
            border-radius:50%;
            filter:blur(32px);
            transition:var(--trans3);
        }

        &:nth-of-type(3n + 1):after{
            animation:blobGrow 2.5s ease-in-out, 
                blobBreathe 10s ease-in-out infinite 2.5s;
        }
        &:nth-of-type(3n + 2):after{
            animation:blobGrow 4s ease-in-out, 
                blobBreathe 8s ease-in-out infinite 4s;
        }
        &:nth-of-type(3n + 3):after{
            animation:blobGrow 7s ease-in-out, 
                blobBreathe 13s ease-in-out infinite 7s;
        }

    }

}

@keyframes blobGrow{
    0%{
        transform:scale(0);
    }
    100%{
        transform:scale(1);
    }
}

@keyframes blobBreathe{
    0%{
        transform:scale(1) rotate(0deg);
    }
    25%{
        transform:scale(0.8) rotate(90deg);
    }
    50%{
        transform:scale(1) rotate(180deg);
    }
    75%{
        transform:scale(0.8) rotate(270deg);
    }
    100%{
        transform:scale(1) rotate(360deg);
    }
}

</style>