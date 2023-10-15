


<template>

    <main>

        <AboutSection />

        <ProjectsSection />

    </main>

</template>



<script lang="ts">
import { defineComponent } from 'vue';
import AboutSection from "./AboutSection.vue";
import ProjectsSection from "./ProjectsSection.vue";

export default defineComponent({
    name: "MainSection",

    components:{
        AboutSection,
        ProjectsSection
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
    padding-top:calc(
        (var(--size6) + var(--size5) * 2) + 
        var(--size7) + var(--size8)
    );

    display:flex;
    flex-direction:column;
    gap:calc(var(--size8) * 2.5);

    & .section-heading{
        width:100%;
        font-size:min(34px, 6vw);
        text-align:center;
    }

    & .tile-heading-capital{
        text-transform:capitalize;
    }

}


@media screen and (width <= 768px){

    main{
        padding-top:var(--size8);
    }

}

@media screen and (width <= 440px){

    main{
        padding-top:calc(
            (var(--size7) + var(--size5) * 2) + 
            var(--size6) + var(--size8)
        );
    }

}

</style>