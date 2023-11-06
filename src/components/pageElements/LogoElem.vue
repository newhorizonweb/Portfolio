


<template>

    <svg class="logo" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 800 800">
        <polyline class="cls-1 logo-shape1" points="643.7 257.6 768.8 31.2 768.8 768.8 400 447.4 31.2 768.8 31.2 31.2 156.3 257.6"/>
        <polyline class="cls-1 logo-shape2" points="261.2 447.4 400 698.6 538.8 447.4"/>
        <circle class="cls-2 logo-shape3" cx="400" cy="218.8" r="117.1"/>

        <line class="cls-1 logo-line logo-line1" x1="227.2" y1="572.8" x2="572.8" y2="227.2"/>
        <line class="cls-1 logo-line logo-line2" x1="572.8" y1="572.8" x2="227.2" y2="227.2"/>
    </svg>

</template>



<script lang="ts">
import { defineComponent } from 'vue'

export default defineComponent({
    name: "LogoElem"
});
</script>



<style lang="scss">

.logo{

    .cls-1,
    .cls-2{
        fill:none;
        stroke-linecap:round;
        stroke-linejoin:round;
        stroke-width:62px;
        transition:var(--trans2);
    }

    .cls-1{
        stroke:#FFF;
    }
    
    .cls-2{
        stroke:var(--color1a);
    }

    .logo-line{
        opacity:0;
        transform-origin:center;
        
    }

}

.nav-expand .nav-logo:hover{

    .logo-shape1{
        transform:translate(50%, -50%) scale(0.3);
    }

    .logo-shape2{
        transform:translate(0, -100%);
    }

    .logo-shape3{
        r:369px;
        cy:400px;
    }

    .logo-line{
        opacity:1;
        transform:rotate(180deg);
        transition-delay:var(--trans2);
    }

}

</style>