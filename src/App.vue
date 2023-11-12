


<template>

<!-- Page Sections -->

    <HeaderSection />

    <MainSection />

    <FooterSection />

<!-- Other Elements -->

    <BgBlobs />

    <CursorBlob />

</template>



<script lang="ts">
import { defineComponent } from 'vue';

import HeaderSection from "./components/header/HeaderSection.vue";
import MainSection from "./components/main/MainSection.vue";
import FooterSection from "./components/footer/FooterSection.vue";

import BgBlobs from "./components/pageElements/BgBlobs.vue";
import CursorBlob from "./components/pageElements/CursorBlob.vue";

export default defineComponent({
    name: "App",

    components:{
        HeaderSection,
        MainSection,
        FooterSection,

        BgBlobs,
        CursorBlob
    },

    data(){
        return{

        }
    },

    mounted(){
        // Scroll the page to the top on load
        if ('scrollRestoration' in history){
            history.scrollRestoration = 'manual';
        }
        window.scrollTo(0, 0);
    }

});
</script>



<style lang="scss">

#app{
    padding-bottom:var(--size7);
}

</style>