


<template>

    <div id="contact-form" class="contact-section wrapper main-section">

        <h2 class="section-heading"
            data-text="Contact">
        </h2>

        <form class="contact-form" ref="contactForm" method="POST">

            <div class="form-input glass-tile">
                <input type="text" class="input-valid"
                    placeholder="Name*" name="name" aria-label="Name Form Input">
            </div>

            <div class="form-input glass-tile">
                <input type="email" class="input-valid" ref="email"
                    placeholder="Email*" name="email" aria-label="Email Form Input">
            </div>

            <div class="form-input glass-tile form-tumbleweed">
                <input type="text" ref="tumbleweed"
                    placeholder="Address" name="address" aria-label="Address Form Input">
            </div>

            <div class="form-input glass-tile">
                <input type="text" class="input-valid"
                    placeholder="Subject*" name="subject" aria-label="Subject Form Input">
            </div>

            <div class="form-input glass-tile">
                <input type="text"
                    placeholder="Company" name="company" aria-label="Company Form Input">
            </div>
                
            <div class="form-input form-textarea glass-tile">
                <textarea class="input-valid"
                    placeholder="Message*" name="message" aria-label="Message Form Input"></textarea>
            </div>

            <div class="form-footer">

                <button class="send-form-btn glass-tile" ref="sendFormBtn"
                    @click="sendForm" aria-label="Submit the contact form">

                    <h3 class="send-btn-txt"
                        data-text="Submit">
                    </h3>

                </button>

                <div class="form-socials">

                    <a href="https://github.com/newhorizonweb"
                        class="form-link form-link1" aria-label="GitHub Link"
                        target="_blank">

                        <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 200 200"><path class="anim-elem1 cls-1" d="M82.6,144.3c-21.1-2.4-43.2-10.5-43.2-46.9a36,36,0,0,1,9.8-25.5,33.5,33.5,0,0,1,.9-25.1s7.9-2.6,26.1,9.7a89.1,89.1,0,0,1,47.5,0c18.1-12.3,26.1-9.7,26.1-9.7a34,34,0,0,1,.9,25.1,36.8,36.8,0,0,1,9.8,25.5c0,36.4-22.1,44.4-43.3,46.8"/><path class="cls-1" d="M117.2,144.2a22.7,22.7,0,0,1,6.4,17.7v26c0,3.2,1.7,5.5,6.5,4.5a95.1,95.1,0,1,0-60.1,0c4.7.9,6.5-2,6.5-4.4V171.9c-26.5,5.7-32-12.8-32-12.8a25.4,25.4,0,0,0-10.7-14c-8.7-5.9.6-5.8.6-5.8a19.4,19.4,0,0,1,14.5,9.8c8.5,14.5,22.1,10.3,27.7,7.9a20.5,20.5,0,0,1,6-12.7"/></svg>
                    </a>

                    <a href="https://www.linkedin.com/in/wojciech-bocho/"
                        aria-label="LinkedIn Link" class="form-link form-link2"
                        target="_blank">

                        <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 200 200"><circle class="anim-elem1 cls-1" cx="27.8" cy="27.8" r="22.7"/><rect class="anim-elem2 cls-1" x="7.7" y="68.6" width="40.6" height="126.25" rx="2"/><path class="cls-1" d="M195,116.1c0-7.9,0-14.2-3.2-23.6A42.5,42.5,0,0,0,171,68.6c-2-1-20.7-10.5-39.9-1-12.7,6.4-18.5,16.8-19.9,24.6h0V70.6a2,2,0,0,0-2-2H74.6a2,2,0,0,0-2,2V192.9a2,2,0,0,0,2,2h34.6c2-1.2,2-1.9,2-2V127.8s-.5-18.2,10.4-25.1a24.2,24.2,0,0,1,24.8-.3c8.5,5.2,9.9,13.7,9.9,27.8v62.6a2,2,0,0,0,2,2H193c2-1.1,2-1.9,2-2V116.1"/></svg>
                    </a>

                </div>

            </div>

        </form>

    </div>

    <div class="form-popup glass-tile" 
        :class="{'popup-visible': popupVisible}">

        <p class="info-msg" ref="infoMsg"></p>

        <CloseBtn
            :glassTile="false"
            @click="popupVisible = false"
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

    data(){
        return{

                /* To Change */

            // Messages
            msgSuccess: "Form submitted successfully. I will contact you as soon as possible!",
            msgFailed: "Something went terribly wrong :( Please try again!",

            msgLongResponse: "Your email is on its way, but it may take a bit longer!",
            msgReallyLongResponse: "It seems like there are some technical difficulties :/",

            msgAttempts: "Too many attempts! Try again in a few minutes.",
            msgEmptyFields: "Didn't you forget about something? :)",
            msgInvalidMail: "Please provide a valid email address!",

            // Popup Time (in seconds)
            popupShowTime: 6, // The time the popup is shown
            popupScrollTime: 0.5, // The time after the popup is hidden after scroling

            // Popup
            popupVisible: false,
            popupTimeout: null as null | number,

            // Mail
            maxAttemptNumber: 8,
            tumbleweed: "address",
            apiResponseDelay: 3, // in seconds
            apiLongResponseDelay: 10, // in seconds
            
                /* In-code */

            // Mail
            mailNumber: 0,
            tooManyAttempts: false,
            emailRegex: /^[a-zA-Z0-9._-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,4}$/,

            // Form
            form: null as null | HTMLFormElement,
            formInpVal: null as null | HTMLInputElement[],
            inputValidCheck: false,

            // Key
            mailProvider: "https://formspree.io/f/",
            key: "eHl5cXZlZ3Y="

        } 
    },

    mounted(){

        // Elements
        this.form = this.$refs.contactForm as HTMLFormElement;
        this.formInpVal = Array.from(this.form.querySelectorAll(".input-valid")) as HTMLInputElement[];

        // Set the popup message in case something is wrong
        (this.$refs.infoMsg as HTMLElement).innerHTML = this.msgFailed;

        // Close the popup faster when scrolling
        document.addEventListener("scroll", () => {
            
            if (this.popupTimeout){
                clearTimeout(this.popupTimeout);
            }

            this.popupTimeout = setTimeout(() => {
                this.popupVisible = false;
            }, this.popupScrollTime * 1000);
       
        });

        // Remove the invalid input class on user input
        this.formInpVal.forEach(input => {
            input.addEventListener("input", () => {

                if (this.formInpVal && this.inputValidCheck){
                    this.formInpVal.forEach(input => {
                        
                        if (input.value.length > 0){
                            input.classList.remove("invalid-input");
                        } else {
                            input.classList.add("invalid-input");
                        }

                    });
                }

            });
        });

    },

    methods:{

            /* Basics */

        decodeKey(){
            return atob(this.key);
        },

            /* Popup */

        showPopup(){

            this.popupVisible = true;

            if (this.popupTimeout){
                clearTimeout(this.popupTimeout);
            }

            this.popupTimeout = setTimeout(() => {
                this.popupVisible = false;
            }, this.popupShowTime * 1000);

        },

        formTxt(message: string){

            const formInfoTxt = (this.$refs.infoMsg as HTMLElement);
            formInfoTxt.innerHTML = message;
            this.showPopup();

        },

            /* Validation */

        removeInvalidClass(){

            if (this.formInpVal){
                this.formInpVal.forEach(input => {
                    input.classList.remove("invalid-input");
                });
            }

        },

        checkMail(){

            const emailInput = this.$refs.email as HTMLInputElement;
            let isValidated = true;

            if (!this.emailRegex.test(emailInput.value)){
                this.formTxt(this.msgInvalidMail);
                emailInput.classList.add("invalid-input");
                isValidated = false;
            }

            return isValidated;
            
        },

        checkValidation(){

            let isValidated = true;
            let emptyFields = false;

            this.removeInvalidClass();
            isValidated = this.checkMail();

            if (this.formInpVal){
                this.formInpVal.forEach(input => {
                    if (input.value.trim() === ""){
                        input.classList.add("invalid-input");
                        isValidated = false;
                        emptyFields = true;
                    }
                });
            }

            if (emptyFields){
                this.formTxt(this.msgEmptyFields);
            }

            return isValidated;

        },

            /* Bot Prevention */

        checkAttemptTimer(){

            const attemptCooldown = localStorage.getItem("attemptCooldown");

            if (attemptCooldown){
                const attemptCooldownVal = parseInt(attemptCooldown, 10);

                if (Date.now() < attemptCooldownVal){
                    this.tooManyAttempts = true;
                } else {
                    this.mailNumber = 0;
                    this.tooManyAttempts = false;
                    localStorage.removeItem("attemptCooldown");
                }
            }

        },

        setAttemptTimer(){

            this.tooManyAttempts = true;
            const time = 1000 * 60 * 1; // 1 min
            
            const attemptCooldown = Date.now() + time;
            localStorage.setItem("attemptCooldown", attemptCooldown.toString());

        },

        preventBot(){

            // Check if the tumbleweed input was filled out by a bot
            if ((this.$refs.tumbleweed as HTMLInputElement).value === ""){
                return false;
            } else {
                this.formTxt(this.msgSuccess);
          
                this.setAttemptTimer();
                return true;
            }

        },

        preventSpam(){

            // Too many submit attempts
            if (this.mailNumber >= this.maxAttemptNumber){
                this.setAttemptTimer();
            }

            if (this.mailNumber >= this.maxAttemptNumber || this.tooManyAttempts){
                this.formTxt(this.msgAttempts);
            }

        },

            /* Send Mail */

        async sendForm(e: Event){

                /* Basics */

            e.preventDefault();
            this.formTxt("");

            // Disable the button
            const sendBtn = this.$refs.sendFormBtn as HTMLElement;
            sendBtn.style.pointerEvents = "none";

            // Enable the check
            this.inputValidCheck = true;

            // Increase the attempt number
            this.mailNumber++;
            
            // Form Data
            const data = new FormData(this.form as HTMLFormElement);
            
                /* Checks */

            // Validation
            const isValidated = this.checkValidation();

            // Spam Prevention
            this.checkAttemptTimer();
            this.preventSpam();

            // Validation Check
            if (!isValidated || this.tooManyAttempts || this.preventBot()){
                sendBtn.style.pointerEvents = "all";
                return;
            }

                /* Form */

            // Delete the tumbleweed input
            data.delete(this.tumbleweed);

            // Delayed API response initiation
            const delayTimer = setTimeout(() => {
                this.formTxt(this.msgLongResponse);
            }, this.apiResponseDelay * 1000);

            const delayTimerLong = setTimeout(() => {
                this.formTxt(this.msgReallyLongResponse);
            }, this.apiLongResponseDelay * 1000);

            // Send the server request
            fetch(this.mailProvider + this.decodeKey(), {

                method: this.form!.method,
                body: data,
                headers:{
                    'Accept': 'application/json'
                }

            })

            // Receive server response
            .then(response => {

                // Clear the timer if the API responded in time
                clearTimeout(delayTimer);
                clearTimeout(delayTimerLong);

                // Handle the API response
                if (response.ok){
                    
                    this.formTxt(this.msgSuccess);
                    this.inputValidCheck = false;
                    this.form!.reset();

                } else {

                    response.json().then(data => {

                        if ('errors' in data){
                            console.log("Form Error: " + 
                                data["errors"].map(
                                        (error: { message: string }) => error["message"]
                                ).join(", ")
                            );
                        }
                        
                    });

                    this.formTxt(this.msgFailed);

                }

                // Enable the button
                sendBtn.style.pointerEvents = "all";

            })

            // Errors
            .catch(error => {

                this.formTxt(this.msgFailed);
                sendBtn.style.pointerEvents = "all";
                console.log("Form Error: " + error);

            });

        }

    }

});
</script>



<style lang="scss">

    /* Form */

.contact-section{
    display:flex;
    flex-direction:column;
    gap:var(--size8);
}

.contact-form{
    display:flex;
    flex-wrap:wrap;
    gap:var(--size6);

        /* Inputs */

    & .form-input{
        flex:40%;
        height:var(--size8);
        display:flex;

        &:hover:before{
            background:var(--borderGrad2);
        }

        &:has(:focus):before{
            background:var(--borderGrad2);
        }

        &:has(:-webkit-autofill):before{
            background:var(--borderGrad3);
        }

        &:has(.invalid-input):before{
            background:var(--borderGrad2b);
        }

        & > *{
            width:100%;
            height:100%;
            padding:0 var(--size6);

            background-color:transparent;
            border:none;
            border-radius:inherit;
            transition:all var(--trans1), box-shadow var(--trans3);

            &:-webkit-autofill{
                -webkit-box-shadow:0 0 0 100px var(--colorBg1c) inset;
                -webkit-text-fill-color:#FFF;
                transition:all var(--trans3), box-shadow var(--trans1);
            }

        }

        &.form-textarea{
            flex:100%;
            height:calc(var(--size8) * 4);
            
            & > *{
                padding:var(--size6);
                resize:none;
            }

        }

        &.form-tumbleweed{
            position:absolute;
            opacity:0;
            pointer-events:none;
        }

        & *::placeholder{
            color:var(--txt-faded3);
        }

    }

        /* Form Footer */

    & .form-footer{
        width:100%;
        display:flex;
        align-items:center;
        gap:var(--size6);

        & .send-form-btn{
            flex:1;
            height:var(--size8);
            cursor:pointer;

            &:hover:before{
                background:var(--borderGrad2);
            }

            & .send-btn-txt{
                font-size:20px;

                &:before{
                    -webkit-text-stroke:1.5px #FFF;
                }

            }

            &:hover .send-btn-txt:before{
                -webkit-text-stroke-color:var(--color1a);
            }

        }

        & .form-socials{
            height:var(--size8);
            display:flex;
            gap:var(--size6);

            & .form-link{
                height:100%;
                aspect-ratio:1/1;
                cursor:pointer;

                & *{
                    fill:none;
                    stroke-linecap:round;
                    stroke-miterlimit:10;

                    stroke:#FFF;
                    stroke-width:10px;
                }

                // Animations are inside the NavbarSection component

                &:hover svg{
                    animation:navAnimElem 2s ease-in-out infinite;
                }

                &.form-link1:hover .anim-elem1{
                    animation:navAnimElem1 2s ease-in-out infinite;
                    transform-origin:100px 144px;
                }

                &.form-link2:hover .anim-elem1{
                    animation:navAnimElem5a 2s ease-in-out infinite;
                    transform-origin:100px 195px;
                }

                &.form-link2:hover .anim-elem2{
                    animation:navAnimElem5b 2s ease-in-out infinite;
                    transform-origin:100px 195px;
                }

            }

        }

    }

}

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

    transition:var(--trans4);
    z-index:1000;
    
    &.popup-visible{
        bottom:var(--size6);
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

    /* Media */

@media screen and (width <= 540px){

    .contact-form{

        & .form-input{
            flex:100%;
        }
        
    }

}

@media screen and (width <= 440px){

    .contact-form{

        & .form-footer{

            & .send-form-btn{

                & .send-btn-txt{
                    font-size:18px;
                }

            }
            
            & .form-socials{
                height:var(--size7);
            }

        }

    }

}

@media screen and (width <= 320px){

    .contact-form{

        & .form-footer{
            flex-direction:column;
            align-items:flex-end;

            & .send-form-btn{
                flex:none;
                width:100%;
            }

            & .form-socials{
                height:var(--size7);
                justify-content:flex-end;
            }

        }

    }

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