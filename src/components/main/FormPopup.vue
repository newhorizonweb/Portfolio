


<template>

    <div class="form-popup glass-tile" 
        :class="{'popup-visible': popupVisible}">

        <p class="info-msg" ref="infoMsg">{{ popupMsg }}</p>

        <CloseBtn
            :glassTile="false"
            @click="this.$emit('closePopup')"
        />

    </div>

</template>



<script lang="ts">
import { defineComponent } from 'vue';
import CloseBtn from "../pageElements/CloseBtn.vue";

export default defineComponent({
    name: "MailForm",

    components:{
        CloseBtn
    },

    props: [
        "popupVisible",
        "popupMsg"
    ],

    data(){
        return{

        } 
    },

    methods:{

        

    }

});
</script>



<style lang="scss">

    /* Form Popup */

main .form-popup{
    width:min(
        1024px, 
        calc(100% - var(--size6) * 2)
    );
    padding:var(--size8);

    position:fixed;
    bottom:calc((var(--size8) * -2) - 3rem);
    left:50%;
    transform:translate(-50%, 0);

    display:flex;
    justify-content:center;
    align-items:center;

    opacity:0;
    animation:formPopupFadeOut var(--trans4) forwards;
    transition:var(--trans4);
    z-index:1000;
    
    &.popup-visible{
        bottom:var(--size6);
        animation:formPopupFadeIn var(--trans4) forwards;
    }

    & .info-msg{
        text-align:center;
        text-wrap:balance;
    }

    & .close-btn{
        position:absolute;
        top:var(--size6);
        right:var(--size6);
    }

}

@keyframes formPopupFadeIn{
    0%{
        opacity:0;
    }
    10%{
        opacity:1;
    }
    100%{
        opacity:1;
    }
}

@keyframes formPopupFadeOut{
    0%{
        opacity:1;
    }
    90%{
        opacity:1;
    }
    100%{
        opacity:0;
    }
}

    /* Media */

@media screen and (width <= 320px){

    main .form-popup{
        padding:var(--size8) var(--size6);

        & .close-btn{
            width:calc(var(--size6) + 4px);

            & span{
                width:var(--size4);
            }

        }

    }

}

</style>