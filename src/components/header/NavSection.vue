


<template>

    <nav>

        <div class="nav-inner glass-tile"
            :class="{
                'page-scrolled': isWindowScrolled,
                'nav-expand': isNavExpand
            }"

            ref="innerNav"
            @click="toggleNav"
            @mousemove="navHoverBorder">

            <div class="nav-logo"
                ref="navCloseBtn">

                <LogoElem />
            </div>

            <NavbarSection />

        </div>

    </nav>

</template>



<script lang="ts">
import { defineComponent } from 'vue'
import NavbarSection from "./NavbarSection.vue";

import LogoElem from "../pageElements/LogoElem.vue";

export default defineComponent({
    name: "NavSection",

    components:{
        NavbarSection,
        LogoElem
    },

    data(){
        return{
            isWindowScrolled: false,
            isNavExpand: false,

            navCloseDistance: 0,
            navCloseCalcDist: 0,
            throtNavCloseDist: 0,
        }
    },

    mounted(){

        // Nav - scrolled view
        window.addEventListener("scroll", () => {
            this.isWindowScrolled = window.scrollY > 0 ? true : false;
        });

        // Nav collapse on page resize
        window.addEventListener("resize", () => {
            this.isNavExpand = false;
        });

        // Nav collapse when clicking outside the nav
        window.addEventListener("click", (e) =>{
            const innerNavElement = this.$refs.innerNav as HTMLElement;

            if (!innerNavElement || 
                (innerNavElement !== e.target &&
                !innerNavElement.contains(e.target as Node))){

                this.isNavExpand = false;
            }
        });

        // Throttle the mousemove border gradient animation
        document.addEventListener("mousemove", (e) => {
            if (!this.throtNavCloseDist){

                this.throtNavCloseDist = setTimeout(() => {
                    this.navCloseDistCalc(e);
                    this.throtNavCloseDist = 0;
                }, 16); // 60+ FPS

            }
        });

    },

    methods:{

        toggleNav(e: MouseEvent){
            if (window.innerWidth <= 768){

                // Check if the clicked element is the navCloseBtn
                const isCloseButton = 
                    (this.$refs.navCloseBtn as HTMLElement).contains(e.target as Node);

                // Check if the clicked element is a nav-link
                const navLinks = document.querySelectorAll(".nav-link");
                let isNavLink = false;
                                
                navLinks.forEach((navLink) => {
                    if (navLink.contains(e.target as Node)){
                        isNavLink = true;
                    }
                });

                // Toggle Nav
                if (this.isNavExpand && (isCloseButton || isNavLink)){
                    this.isNavExpand = false;
                } else if (!this.isNavExpand){
                    this.isNavExpand = true;
                }

            }
        },

        navCloseDistCalc(e: MouseEvent){
            
            if (window.innerWidth <= 768){
                const innerNav = this.$refs.innerNav as HTMLElement;
                if (!innerNav || !e.target) return;

                if (e.target === innerNav ||
                    innerNav.contains(e.target as Node)){
                           
                    // Get the close button position data
                    const closeBtnRect = (this.$refs.navCloseBtn as HTMLElement).getBoundingClientRect();
                    const innerNavRect = innerNav.getBoundingClientRect();

                    // Distance
                    const dx = Math.max(0, e.clientX < closeBtnRect.left 
                        ? closeBtnRect.left - e.clientX 
                        : e.clientX - closeBtnRect.right);
                    const dy = Math.max(0, e.clientY < closeBtnRect.top 
                        ? closeBtnRect.top - e.clientY 
                        : e.clientY - closeBtnRect.bottom);

                    // Calculate the distance
                    const distToCloseBtn = Math.sqrt(dx * dx + dy * dy);
                    const maxDist = Math.hypot(innerNavRect.width, innerNavRect.height);

                    // Ensure the distance is within bounds
                    this.navCloseDistance = Math.max(0, 
                        Math.min((100 * (1 - (distToCloseBtn / maxDist))), 100)
                    );
                        
                    this.navCloseCalcDist = 
                        50 - (5/9) * (this.navCloseDistance - 100);

                } else {
                    this.navCloseDistance = 0;
                    this.navCloseCalcDist = 0;
                }

            }
            
        }

    },

    watch:{
        navCloseCalcDist(newVal){
            if (newVal > 0){
                document.body.style.setProperty("--navDistColor", 
                    `${this.navCloseDistance * 0.8}%`);
                document.body.style.setProperty("--navDistBorder", 
                    `${newVal}%`);
            } else {
                document.body.style.setProperty("--navDistColor", "0");
                document.body.style.setProperty("--navDistBorder", "100%");
            }
        }
    }

});
</script>



<style lang="scss">

nav{
    position:relative;
    z-index:9999;
    transition:opacity var(--trans3);
}

.modal-mode nav{
    opacity:0;
}

.nav-placeholder{
    height:calc((var(--size6) * 2) + var(--size8));
    margin-top:var(--size7);
    transition:var(--trans2);
}

nav .nav-inner{
    --navbar-width:160px;

    width:min(1024px, calc(100% - (var(--size6) * 2)));
    padding:var(--size6);
    margin:0 var(--size6);
    
    position:fixed;
    top:var(--size7);
    right:calc(50% - var(--size6));
    transform:translate(50%, 0);

    display:flex;
    justify-content:space-between;

    transition:all var(--trans2), 
        width 0s, 
        margin 0s,
        right 0s, 
        top 0s,
        transform 0s;

    & .nav-logo{
        display:flex;
    }

    & .logo{
        width:var(--size8);
        aspect-ratio:1/1;
        transition:var(--trans2);
    }

    & .navbar{
        display:flex;
        justify-content:space-between;
        gap:var(--size8);
        transition:all var(--trans2), 
            right 0s, 
            opacity 0s;

        & .nav-links{
            display:flex;
            align-items:center;
            gap:var(--size6);
        }

    }

    & .nav-link{
        display:flex;
        align-items:center;
        gap:var(--size3);
        cursor:pointer;

        &:hover .nav-link-txt:before{
            -webkit-text-stroke-color:var(--color1a);
        }

    }

    & .nav-links-page svg{
        display:none;
    }

    & .nav-links-social .nav-link{
        width:var(--size7);
        height:var(--size7);

        display:flex;
        justify-content:center;
        align-items:center;

        & svg{
            height:100%;
        }

        & .nav-link-txt{
            display:none;
        }

    }

    &.page-scrolled{
        padding:var(--size5) var(--size6);

        & .logo{
            width:var(--size6);
        }

        & .nav-links-social .nav-link{
            height:var(--size6);
        }

    }

}

@media screen and (width <= 768px){

    .nav-placeholder{
        height:0;
        margin-top:0;
    }

    nav .nav-inner{
        width:calc(var(--size7) + (var(--size5) * 2));
        margin:0;
        padding:var(--size5) !important;

        top:var(--size6);
        right:var(--size6);
        transform:translate(0, 0);

        flex-direction:column;
        align-items:flex-end;
        gap:0;

        background:var(--colorBg2d);
        transition:all 0.25s, 
            margin 0s,
            right 0s, 
            top 0s,
            transform 0s;
        overflow:hidden;

        &:after{
            content:"";
            padding:var(--border);
            position:absolute;
            
            inset:0;
            mask:linear-gradient(#000 0 0) content-box, 
                linear-gradient(#000 0 0);
            -webkit-mask:linear-gradient(#000 0 0) content-box, 
                linear-gradient(#000 0 0);
            -webkit-mask-composite:xor;
            mask-composite:exclude;

            border-radius:var(--size6);
            background:linear-gradient(to top right,
                transparent 0%,
                transparent var(--navDistBorder),
                rgb(255, 255, 255, var(--navDistColor) ) 100%);

            opacity:0;
            transition:var(--trans2);
            pointer-events:none;
        }

        & .nav-logo{
            cursor:pointer;
        }

        & .logo{
            width:var(--size7);
        }

        & .navbar{
            height:0;
            width:var(--navbar-width);

            position:relative;
            top:0;
            right:-100%;

            flex-direction:column;
            align-items:flex-end;
            gap:var(--size5);
            opacity:0;

            & .nav-links{
                width:100%;
                flex-direction:column;
                align-items:stretch;
                gap:var(--size5);
            }

        }

        & .nav-link{
            width:100%;

            & svg{
                min-width:var(--size7);
                width:var(--size7);
                aspect-ratio:1/1;
            }

            & .nav-link-txt{
                flex:100%;
                text-align:right;
            }

        }

        & .nav-links-page svg{
            display:block;
        }

        & .nav-links-social .nav-link{
            width:100%;

            & .nav-link-txt{
                display:block;
            }

        }

        &.page-scrolled{

            & .logo{
                width:var(--size7);
            }

            & .nav-links-social .nav-link{
                height:var(--size7);
            }

        }

        &.nav-expand{
            width:calc(var(--navbar-width) + (var(--size5) * 2));
            gap:var(--size7);

            &:hover:after{
                opacity:1;
            }

            & .navbar{
                height:calc(
                    (var(--size7) * 6) +    /* Link */
                    (var(--size5) * 5)      /* Nav Links Gaps */
                );
                right:0;
                opacity:1;
            }

        }

    }
    
}

@media screen and (width <= 440px){

    nav .nav-inner{
        --navbar-width:145px;
    }

}

@media screen and (width <= 320px){

    nav .nav-inner{
        --navbar-width:135px;
    }

}

</style>