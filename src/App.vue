


<template>

<!-- Page Sections -->

    <HeaderSection />

    <MainSection />

    <FooterSection />

<!-- Other Elements -->

    <BgBlobs />

</template>



<script lang="ts">
import { defineComponent } from 'vue';
import HeaderSection from "./components/header/HeaderSection.vue";
import MainSection from "./components/main/MainSection.vue";
import FooterSection from "./components/footer/FooterSection.vue";

import BgBlobs from "./components/pageElements/BgBlobs.vue";

export default defineComponent({
    name: "App",

    components: {
        HeaderSection,
        MainSection,
        FooterSection,
        BgBlobs
    },

    data(){
        return{

        }
    }

});
</script>



<style lang="scss">



</style>