


<template>

    <main>

        <AboutSection />

    </main>

</template>



<script lang="ts">
import { defineComponent } from 'vue';
import AboutSection from "./AboutSection.vue";

export default defineComponent({
    name: "MainSection",

    components:{
        AboutSection
    },

    data(){
        return{

        }
    },

    methods:{
        
    }

});
</script>



<style lang="scss">

main{
    padding-top:150px;

    & .section-heading{
        width:100%;
        text-align:center;
    }

    & .tile-heading-capital{
        text-transform:capitalize;
    }

}

</style>