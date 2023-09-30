


<template>

    <footer>

        <p>v{{ appVersion }}</p>

    </footer>

</template>



<script lang="ts">
import { defineComponent } from 'vue'
import { version } from "../../../package.json";

export default defineComponent({
    name: "MainSection",

    components:{

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



</style>