


<template>

    <footer class="wrapper glass-tile">

        <div class="footer-logo"
            @click="logoScroll">

            <LogoElem />

        </div>

        <div class="footer-version">
            <p>Portfolio v{{ appVersion }}</p>
            <p>© 2023 Wojciech Bocho</p>
        </div>
    </footer>

</template>



<script lang="ts">
import { defineComponent } from 'vue'
import { version } from "../../../package.json";
import LogoElem from "../pageElements/LogoElem.vue";

export default defineComponent({
    name: "MainSection",

    components:{
        LogoElem
    },

    data(){
        return{
            appVersion: version
        }
    },

    methods:{

        logoScroll(){

            if (window.innerWidth > 768){
                window.scrollTo({
                    top: 0,
                    behavior: "smooth"
                });
            }

        }
        
    }

});
</script>



<style lang="scss">

footer.wrapper{
    margin-top:calc(var(--size8) * 2.5);
    padding:var(--size6);

    display:flex;
    justify-content:space-between;
    align-items:center;

    transition:opacity var(--trans3);

    & .footer-logo{
        height:var(--size8);
        display:flex;
        cursor:var(--cursorHover);

        & .logo{
            height:100%;
        }

        &:hover .logo-shape3{
            animation:logoHeadAnim 2s ease-in-out infinite; // NavSection animation
        }

    }

    & .footer-version{
        display:flex;
        flex-direction:column;
        align-items:flex-end;
        gap:var(--size1);

        & p{
            font-size:16px;
        }

    }

}

body:has(.section-out) footer{
    // Prevent the footer from flashing while scrolling the page
    opacity:0;
}

.modal-mode footer{
    opacity:0;
}

@media screen and (width <= 440px){

    footer.wrapper{
        flex-direction:column;
        gap:var(--size6);

        & .footer-version{
            align-items:center;
        }

    }

}

</style>