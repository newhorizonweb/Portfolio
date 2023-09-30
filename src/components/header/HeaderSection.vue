


<template>

    <header>

        <NavSection />

    </header>

</template>



<script lang="ts">
import { defineComponent } from 'vue'
import NavSection from "./NavSection.vue";

export default defineComponent({
    name: "HeaderSection",

    components:{
        NavSection
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



</style>