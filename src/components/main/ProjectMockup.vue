


<template>

    <div class="mockup-outer">

        <div class="mockup-mode"
            :class="{'toggle-disabled': mockupChange}"
            @click="desktopMockup = !desktopMockup">

            <h4 class="toggle-txt toggle-txt-desktop" data-text="Desktop"></h4>
            <h4 class="toggle-txt toggle-txt-slash" data-text="/"></h4>
            <h4 class="toggle-txt toggle-txt-mobile" data-text="Mobile"></h4>

        </div>

        <div class="mockup"
            :class="{
                'desktop-mockup': desktopMockup,
                'mockup-change': mockupChange}
            ">

            <span class="phone-elem"></span>
            <span class="phone-elem"></span>
            <span class="phone-elem"></span>
            <span class="phone-elem"></span>
            <span class="phone-elem"></span>

            <span class="stand-elem"></span>
            <span class="stand-elem"></span>

            <div class="mockup-inner hide-scrollbar">
                <img class="mockup-img"
                    :src="mockupImg" 
                    alt="Project Mockup">
            </div>

            <div class="mockup-trans">
                <LogoElem />
            </div>

        </div>
    </div>

</template>



<script lang="ts">
import { defineComponent } from 'vue';
import LogoElem from "../pageElements/LogoElem.vue";

export default defineComponent({
    name: "ProjectMockup",

    components:{
        LogoElem
    },

    props:[
        "data"
    ],

    data(){
        return{
            desktopMockup: true,
            mockupChange: false,
            mockupImg: ""
        } 
    },

    mounted(){

        if (window.innerWidth <= 768){
            this.desktopMockup = false;
            this.mockupImg = this.data.mobileMockup;
        } else {
            this.mockupImg = this.data.desktopMockup;
        }

    },

    methods:{

        changeMockupImg(){

            // Set the mockup to the transition mode
            this.mockupChange = true;

            // Remove the transition mode
            setTimeout(() => {
                this.mockupChange = false;
            }, 750)

            // Change the mockup image
            setTimeout(() => {
                if (this.desktopMockup === true){
                    this.mockupImg = this.data.desktopMockup;
                } else {
                    this.mockupImg = this.data.mobileMockup;
                }
            }, 275);

        }

    },

    watch:{

        desktopMockup(){
            this.changeMockupImg();
        }

    }

});
</script>



<style lang="scss">

    /* Outer Mockup */

.mockup-outer{
    --mockupSize:var(--size3);

    display:flex;
    justify-content:center;
    flex-wrap:wrap;
    transition:var(--trans3);
    
    &:has(.desktop-mockup){
        padding-bottom:calc(var(--mockupSize) * 4)
    }

}

.mockup-mode{
    width:100%;
    margin-bottom:var(--size6);

    display:flex;
    justify-content:center;
    gap:var(--size4);
    cursor:pointer;

    & .toggle-txt{
        font-size:min(26px, 5vw);

        &.toggle-txt-desktop:before{
            -webkit-text-stroke:3px var(--color1a);
        }

    }

    &.toggle-disabled{
        pointer-events:none;

        & .toggle-txt-slash:before{
            -webkit-text-stroke-color:var(--color1a);
        }

    }

}

.modal-content:not(:has(.desktop-mockup)){

    & .toggle-txt-desktop:before{
        -webkit-text-stroke-color:#FFF;
    }

    & .toggle-txt-mobile:before{
        -webkit-text-stroke-color:var(--color1a);
    }

}

    /* Mockup */

.mockup{
    width:min(380px, 100%);
    aspect-ratio:9/18;
    margin:0 var(--size1);
    position:relative;
    
    border:solid var(--mockupSize) #FFF;
    border-radius:var(--size7);
    transition:all 0.75s ease-in-out,
        margin var(--trans3);
    
        /* Desktop Mode */

    &.desktop-mockup{
        width:100%;
        aspect-ratio:16/9;
        margin:0;

        & .phone-elem{
            width:0;
            left:calc(var(--mockupSize) * -1);

            &:nth-of-type(4){
                right:calc(var(--mockupSize) * -1);
            }

            &:nth-of-type(5){
                transform:translate(-50%, 0) scale(0);
            }

        }

        & .stand-elem{
            
            &:nth-of-type(6){
                height:calc(var(--mockupSize) * 2.5 + 1px);
                top:calc(
                    100% - 1px +
                    var(--mockupSize)
                );
            }

            &:nth-of-type(7){
                height:calc(var(--mockupSize) * 1.5 + 1px);
                top:calc(
                    100% - 1px + 
                    var(--mockupSize) + 
                    (var(--mockupSize) * 2.5)
                );
            }

        }

    }

    & .stand-elem{
        height:0;
        position:absolute;
        left:50%;
        transform:translate(-50%, 0);

        background-color:#FFF;
        transition:var(--trans3);

        &:nth-of-type(6){
            width:8%;
            top:calc(100% + var(--mockupSize));
        }

        &:nth-of-type(7){
            width:40%;
            top:calc(100% + var(--mockupSize));
            border-radius:200px;
        }

    }

        /* Mobile Mode */

    & .phone-elem{
        width:calc(var(--size1) + 1px);
        position:absolute;
        left:calc((var(--mockupSize) + var(--size1)) * -1);

        background-color:#FFF;
        border-radius:100px 0 0 100px;
        transition:var(--trans3);
        z-index:100;

        &:nth-of-type(1){
            height:calc(var(--mockupSize) * 2);
            top:20%;
        }
        &:nth-of-type(2){
            height:calc(var(--mockupSize) * 3);
            top:calc(
                20% + 
                (var(--mockupSize) * 2) +   /* btn 1 */
                (var(--mockupSize) * 3)     /* gap 1 */
            );
        }
        &:nth-of-type(3){
            height:calc(var(--mockupSize) * 3);
            top:calc(
                20% + 
                (var(--mockupSize) * 2) +   /* btn 1 */
                (var(--mockupSize) * 3) +   /* gap 1 */
                (var(--mockupSize) * 3) +   /* btn 2 */
                (var(--mockupSize) * 2)     /* gap 2 */
            );
        }

        &:nth-of-type(4){
            height:calc(var(--mockupSize) * 5);
            top:30%;
            left:auto;
            right:calc((var(--mockupSize) + var(--size1)) * -1);
            border-radius:0 100px 100px 0;
        }

        &:nth-of-type(5){
            width:var(--size4);
            height:var(--size4);
            top:calc(var(--mockupSize) + var(--size2));
            left:50%;
            transform:translate(-50%, 0);
            border-radius:50%;
        }

    }

        /* Mockup Transition Screen */

    & .mockup-trans{
        width:calc(100% + 2px);
        height:calc(100% + 2px);

        position:absolute;
        top:-1px;
        top:-1px;

        display:flex;
        justify-content:center;
        align-items:center;

        opacity:0;
        background:var(--colorGrad1);
        border-radius:calc(var(--size7) - var(--mockupSize));

        transition:0.25s ease-in-out;
        pointer-events:none;
        z-index:10;

        & .logo{
            width:min(100px, 40%);
        }

    }

    &.mockup-change .mockup-trans{
        opacity:1;
    }
    
        /* Mockup Inner */

    & .mockup-inner{
        width:calc(100% + 2px);
        height:calc(100% + 2px);
        margin:-1px;

        display:flex;
        align-items:flex-start;

        box-shadow:inset 0 0 0 3px white;
        border-radius:calc(var(--size7) - var(--mockupSize));
        overflow:auto;

        & .mockup-img{
            width:100%;
        }

    }

}

@media screen and (width <= 768px){

    .mockup{
        aspect-ratio:9/16;

        &.desktop-mockup{
            aspect-ratio:16/10;
        }

    }

}

@media screen and (width <= 540px){

    .mockup-outer{
        --mockupSize:var(--size2);
    }

    .mockup{

        &.desktop-mockup{
            aspect-ratio:4/3;
        }

    }

}

</style>