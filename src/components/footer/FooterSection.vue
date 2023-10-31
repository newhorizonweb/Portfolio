


<template>

    <footer class="wrapper glass-tile">
        <LogoElem />

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

    & .logo{
        height:var(--size8);
    }

    & .footer-version{
        display:flex;
        flex-direction:column;
        align-items:flex-end;
        gap:var(--size1);
    }

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