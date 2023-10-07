


<template>

    <header>
        <NavSection />

        <div class="hero wrapper" ref="heroSection">

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
            scrollDuration: 2000, // in ms
            framerate: 60, // FPS

            // Auto Scroll Variables
            isAutoScrolling: false,
            topPage: true,
            scrollPos: 0,

            // Other
            pageScrollVal: 0,
            isMounted: false
        }
    },

    mounted(){

        this.isMounted = true;

        window.addEventListener("scroll", () => {
            this.pageScrollVal = window.scrollY as number;

            this.parallaxHero();
            this.heroOpacity();

            this.autoScrollDirection();
        });

    },

    methods:{

            /* Parallax */

        parallaxHero(){
            (this.$refs.heroSection as HTMLElement).style.top = 
                `-${this.pageScrollVal * 0.4}px`;
        },

        heroOpacity(){
            const windowHeight = window.innerHeight;
            (this.$refs.heroSection as HTMLElement).style.opacity = 
                `${100 - (this.pageScrollVal / windowHeight * 100)}%`;
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
            window.removeEventListener('wheel', this.preventScroll);
            window.removeEventListener('touchmove', this.preventScroll);
        },

        preventScrolling(){
            window.addEventListener('wheel', this.preventScroll, { passive: false });
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
            if (this.isAutoScrolling) return;

            // Do not execute the code when a nav-link was clicked
            if (document.body.classList.contains("nav-link-clicked")){
                this.topPage = false;
                return;
            }

            // Check the scroll direction
            if (!this.topPage && direction === "down") return;
            if (this.topPage && direction === "up" || 
                window.scrollY >= window.innerHeight && direction === "up"){
                return;
            }

                /* Settings */

            this.isAutoScrolling = true;

            // Check if the page is at the top position
            this.isTopPage(direction);

            // Scroll start/end position
            const startPosition = window.scrollY;
            const endPosition = direction === "down" ? window.innerHeight : 0;
            
            // The number of frames
            const totalFrames = (this.scrollDuration / 1000) * this.framerate;
            
            // Disable scrolling
            this.preventScrolling();

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
                const progress = i / totalFrames;
                const desiredScrollTop = 
                    startPosition + (endPosition - startPosition) * easing(progress);

                window.scrollTo({
                    top: desiredScrollTop
                });

                requestAnimationFrame(animateScroll);
                i++;

            };

            // Start the animation
            animateScroll();
        }

    }

});
</script>



<style lang="scss">

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