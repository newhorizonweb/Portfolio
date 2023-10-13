


<template>

    <footer class="wrapper glass-tile">
 
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

footer.wrapper{
    margin-top:calc(var(--size8) * 2.5);
    padding:var(--size6);
}

</style>