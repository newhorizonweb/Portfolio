


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
        });
    },

    methods:{

        parallaxHero(){
            (this.$refs.heroSection as HTMLElement).style.top = 
                `-${this.pageScrollVal * 0.75}px`;
        },

        heroOpacity(){
            const windowHeight = window.innerHeight;
            (this.$refs.heroSection as HTMLElement).style.opacity = 
                `${100 - (this.pageScrollVal / windowHeight * 100)}%`;
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