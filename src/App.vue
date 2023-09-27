


<template>

    Portfolio
    <p>v{{ appVersion }}</p>


</template>



<script lang="ts">
import { defineComponent } from 'vue';
import { version } from '../package.json'

export default defineComponent({
    name: "App",

    data(){
        return{
            appVersion: version
        }
    }

});
</script>



<style lang="scss">



</style>
