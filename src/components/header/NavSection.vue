


<template>

    <nav class="wrapper glass-tile">

        <LogoElem />

    </nav>

</template>



<script lang="ts">
import { defineComponent } from 'vue'
import LogoElem from "../pageElements/LogoElem.vue";

export default defineComponent({
    name: "NavSection",

    components:{
        LogoElem
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