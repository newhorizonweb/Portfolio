


<template>

    <header>
        <NavSection />

        <div class="hero wrapper" 
            :class="{'parallax': !topPage}" 
            ref="heroSection">

            <div class="hero-title">
                <h1 class="pro-title"
                    data-text="Web-Dev & Designer">
                </h1>

                <NameHeading 
                    :pageScrollVal="pageScrollVal"
                    :isMounted="isMounted"
                />
            </div>

            <div class="hero-icon-div"></div>

        </div>
    </header>

</template>



<script lang="ts">
import { defineComponent } from 'vue'
import NavSection from "./NavSection.vue";
import NameHeading from "./NameHeading.vue";

export default defineComponent({
    name: "HeaderSection",

    components:{
        NavSection,
        NameHeading
    },

    data(){
        return{
            // Auto Scroll Animation Settings
            scrollDuration: 1500, // in ms
            framerate: 60, // FPS, max 100 - JS can't handle more (timing issue)

            // Auto Scroll Variables
            isAutoScrolling: false,
            topPage: true,
            scrollPos: 0,

            // Other
            startY: 0,
            pageScrollVal: 0,
            isMounted: false
        }
    },

    mounted(){

        this.isMounted = true;
        
        window.addEventListener("scroll", this.preventUserScroll, { passive: false });

        window.addEventListener('touchstart', (e) => {
            this.startY = e.touches[0].clientY;
        });

        window.addEventListener('touchmove', this.touchScrollThrottle, { passive: false });

    },

    methods:{

            /* Page Scroll */

        preventUserScroll(e: Event){

            this.pageScrollVal = window.scrollY as number;

            // Don't allow user scrolling during the auto scroll
            this.autoScrollDirection();

            if (window.scrollY <= window.innerHeight){
                e.preventDefault();
            }

        },

        touchScrollThrottle(e: TouchEvent){

            if (!this.isAutoScrolling && window.scrollY <= window.innerHeight){

                // Prevent default scrolling
                e.preventDefault();

                // Calculate the touch scroll delta
                const currentY = e.touches[0].clientY;
                const deltaY = this.startY - currentY;

                // Adjust the page's scroll position
                window.scrollBy(0, deltaY);

                // Update startY
                this.startY = currentY;

            }

        },

            /* Auto Scroll */

        autoScrollDirection(){
            // Current scroll position
            const currPos = window.scrollY;

            // Check the scroll direction
            const scrollDir = this.scrollPos > currPos ? "up" : "down";
            this.autoScroll(scrollDir);

            // Set the scroll position to the current one to compare it later
            this.scrollPos = currPos;
        },

        preventScroll(e: Event){
            e.preventDefault();
        },

        enableScrolling(){
            document.documentElement.classList.remove("no-scroll");
            window.removeEventListener('scroll', this.preventScroll);
            window.removeEventListener('touchmove', this.preventScroll);
        },

        preventScrolling(){
            document.documentElement.classList.add("no-scroll");
            window.addEventListener('scroll', this.preventScroll, { passive: false });
            window.addEventListener('touchmove', this.preventScroll, { passive: false });
        },

        isTopPage(direction: string){
            if (direction === "down"){
                this.topPage = false;
            } else if (direction === "up" && 
                window.scrollY <= window.innerHeight){
                this.topPage = true;
            }
        },

        autoScroll(direction: string){

                /* Execution Conditions */
    
            // Do not execute the code while auto scrolling
            // And check the direction conditions
            if (this.isAutoScrolling ||
                !this.topPage && direction === "down" ||
                this.topPage && direction === "up" || 
                window.scrollY >= window.innerHeight && direction === "up"){
                return;
            }

            // Do not execute the code when a nav-link was clicked
            if (document.body.classList.contains("nav-link-clicked")){
                this.topPage = false;
                return;
            }

                /* Settings */

            // Disable scrolling
            this.preventScrolling();

            this.isAutoScrolling = true;

            // Check if the page is at the top position
            this.isTopPage(direction);

            // Scroll start/end position
            const startPosition = window.scrollY;
            const endPosition = direction === "down" ? window.innerHeight + 1 : 0;
            const scrollRange = endPosition - startPosition;
            
            // Frames
            const totalFrames = (this.scrollDuration / 1000) * this.framerate;
            const frameInterval = 1000 / this.framerate;

            // Easing (slower end of the animation)
            const easing = (t: number) => 1 - (1 - t) * (1 - t);
            let i = 0;

                /* Scroll Animation */

            const animateScroll = () => {

                if (i > totalFrames) {
                    // Enable scrolling after the animation
                    this.enableScrolling();

                    // Set the animation as finished
                    this.isAutoScrolling = false;
                    return; 
                }

                // Update the scroll position
                const scrollTo = startPosition + scrollRange * easing(i / totalFrames);

                window.scrollTo({
                    top: scrollTo
                });
                
                i++;
                setTimeout(() => {
                    requestAnimationFrame(animateScroll);
                }, frameInterval)

            };

            // Start the animation
            requestAnimationFrame(animateScroll);
        }

    }

});
</script>



<style lang="scss">

.no-scroll{
    overflow:hidden;
}

header{
    height:100dvh;

    & .hero{
        width:min(
            1024px,
            calc(100% - (var(--size6) * 2))
        );
        height:100%;
        padding:0;

        position:fixed;
        top:0;
        left:50%;
        transform:translate(-50%, 0);
        z-index:10;

        display:flex;
        justify-content:space-between;
        align-items:center;

        transition:top 2s ease-out,
            opacity 1.5s ease-out;

        & .hero-title{
            display:flex;
            flex-direction:column;
            gap:var(--size8);

            & .pro-title{
                font-size:min(38px, 3.5vw);

                &:before{
                    -webkit-text-stroke:min(2px, 0.2vw) white;
                }

            }

            & .name-heading{
                width:min(600px, 55vw);
            }

        }

        & .hero-icon{
            width:min(300px, 27.5vw);

            & .cls-1{
                fill:none;
                stroke:#fff;
                stroke-miterlimit:10;
                stroke-width:0.7px;
            }

        }

    }

    & .hero.parallax{
        top:-60vh;
        opacity:0;
    }

}

@media screen and (width <= 768px){
 
    header{

        & .hero{

            & .hero-title{
                gap:var(--size7);
            }

        }

    }

}

@media screen and (width <= 540px){
 
    header{

        & .hero{
            flex-direction:column;
            justify-content:center;
            align-items:flex-start;
            gap:var(--size8);

            & .hero-title{
                width:100%;
                gap:var(--size6);

                & .pro-title{
                    font-size:6vw;

                    &:before{
                        -webkit-text-stroke:min(2px, 0.4vw) white;
                    }

                }

                & .name-heading{
                    width:100%;
                }

            }

            & .hero-icon-div{
                width:100%;
                display:flex;
                justify-content:center;
            }

            & .hero-icon{
                align-self:center;
                width:min(200px, 50%);

                & .cls-1{
                    fill:none;
                    stroke:#fff;
                    stroke-miterlimit:10;
                    stroke-width:0.7px;
                }

            }

        }

    }

}

</style>