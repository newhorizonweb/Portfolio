


<template>

    <main>

    <!-- About -->

        <div ref="aboutSection" id="about-section"
            class="about-section wrapper main-section">

            <AboutSection
                v-if="wasSectionLoaded['about-section']"
            />

        </div>

    <!-- Dev Projects -->

        <div ref="devTilesSection" id="dev-projects"
            class="tile-section wrapper main-section">
        
            <TilesSection
                v-if="wasSectionLoaded['dev-projects']"
                sectionTitle="Web-Dev Projects"

                :modalComp="ProjectModal"
                :contents="devProjects"
            />

        </div>

    <!-- Graphic Design -->

        <div ref="designTilesSection" id="design-projects"
            class="tile-section wrapper main-section">

            <TilesSection
                v-if="wasSectionLoaded['design-projects']"
                sectionTitle="Graphic Design"

                :modalComp="DesignModal"
                :contents="graphicDesign"
            />

        </div>

    <!-- Contact Form -->

        <div id="contact-form" class="contact-section wrapper main-section">

            <MailForm
                v-if="wasSectionLoaded['contact-form']"
            />

        </div>

    </main>

</template>



<script lang="ts">
import { defineComponent, markRaw } from 'vue';

import AboutSection from "./AboutSection.vue";
import TilesSection from "./TilesSection.vue";

import ProjectModal from "./ProjectModal.vue";
import DesignModal from "./DesignModal.vue";

import MailForm from "./MailForm.vue";

export default defineComponent({
    name: "MainSection",

    components:{
        AboutSection,
        TilesSection,
        MailForm
    },

    data(){
        return{

                /* Web Developer Projects */
            
            devProjects:[

                {
                    title: "Cookbook",
                    imgSrc: this.path('dev-projects/uverit-logo.svg'),

                    gitHubLink: "https://github.com/newhorizonweb/Uverit-Cookbook",
                    pageLink: "",
                    
                    mobileMockup: this.path('dev-projects/cookbook-mobile.webp'),
                    desktopMockup: this.path('dev-projects/cookbook-desktop.webp'),

                    overview:[
                        "Uverit Cookbook is a digital platform offering a vast collection of recipes and products.",
                        "Equipped with an interactive, multifunctional calculator, it allows users to determine nutritional values and compute insulin requirements.",
                        "It serves as a convenient hub for tracking calorie consumption, crafting unique recipes, and bookmarking favorite products."
                    ],

                    about:[
                        "This is my first major project. Primarily, it was supposed to be a simple cookbook app without any additional features. Then, I added the ability to save products, group everything into categories, search for everything with tags, and much more.",
                        "I had been using jQuery for quite some time, but it was my first big PHP + SQL project.",
                        "I learned a lot - especially how to integrate back-end with front-end, use databases in practice and how to do cool stuff with js, like scroll effects and parallax effect.",
                        "This is also the project where I learned a lot about user interface, user experience and SEO."
                    ],

                    stack:[
                        "HTML & CSS",
                        "JavaScript & AJAX",
                        "jQuery",
                        "PHP & SQL"
                    ]
                },

                {
                    title: "Logo Test",
                    imgSrc: this.path('dev-projects/uverit-logo.svg'),

                    gitHubLink: "https://github.com/newhorizonweb/Uverit-Logo-Test",
                    pageLink: "https://newhorizonweb.github.io/Uverit-Logo-Test/",

                    mobileMockup: this.path('dev-projects/logo-test-mobile.webp'),
                    desktopMockup: this.path('dev-projects/logo-test-desktop.webp'),

                    overview:[
                        "Uverit Logo Test is a program designed to deconstruct logos into simple, easily understandable elements.",
                        "This provides an effective method for identifying areas that may require improvements. Additionally, it can help in making adjustments to better accommodate individuals with disabilities."
                    ],

                    about:[
                        "Since I do graphic design, I needed a reliable way to test and display logos. The idea was simple - create a program that can show how a logo could be seen by different people or in different circumstances.",
                        "Not only are there sections for color-blindness simulation, but also blurriness and a mockup with the logo as an icon.",
                        "This project required a broad knowledge of image manipulation in JavaScript, colors, perception, and user experience.",
                        "I really enjoyed the creative process, as well as building this application. Learning about things not directly related to web development gave me a fresh perspective on how many of us perceive design and websites."
                    ],

                    stack:[
                        "HTML & CSS",
                        "JavaScript",
                        "TypeScript"
                    ]
                },

                {
                    title: "SkillPeak",
                    imgSrc: this.path('dev-projects/uverit-logo.svg'),

                    gitHubLink: "https://github.com/newhorizonweb/Uverit-SkillPeak",
                    pageLink: "https://newhorizonweb.github.io/Uverit-SkillPeak/",

                    mobileMockup: this.path('dev-projects/skillpeak-mobile.webp'),
                    desktopMockup: this.path('dev-projects/skillpeak-desktop.webp'),

                    overview:[
                        "Uverit SkillPeak is a user-friendly program that provides a swift and hassle-free experience for creating resumes.",
                        "Designed for simplicity, it also provides the flexibility to craft a unique and professional representation of one's skills and experiences."
                    ],

                    about:[
                        "I figured that the best way to showcase my skills is to create a program that will allow me to, well... showcase my skills.",
                        "From uploading images, to utilizing user input, to implementing the latest technologies. SkillPeak is an easy-to-use resume creator with a lot of cool features. Usually, the online tools lack some specific element or are behind a paywall. When creating this project, I wanted to include every essential feature, so the user experience is complete. The process of creating a resume should be as simple as possible - the main focus should lie on presenting one's skills and experience, not on trying to figure out the layout, reading multiple pop-ups, and learning that you need to pay or register to download your resume after it was completed.",
                        "I learned a lot about self-presentation and creating resumes. I also acquired useful knowledge about the SVG animations and user interface based on the input. I also utilized the latest features, such as container queries for the PDF preview."
                    ],

                    stack:[
                        "HTML & CSS",
                        "JavaScript",
                        "TypeScript",
                        "SASS (SCSS)"
                    ]

                },

                {
                    title: "Color Palette",
                    imgSrc: this.path('dev-projects/uverit-logo.svg'),

                    gitHubLink: "https://github.com/newhorizonweb/Uverit-Color-Palette",
                    pageLink: "https://newhorizonweb.github.io/Uverit-Color-Palette/index.html",

                    mobileMockup: this.path('dev-projects/color-palette-mobile.webp'),
                    desktopMockup: this.path('dev-projects/color-palette-desktop.webp'),

                    overview:[
                        "Uverit Color Palette showcases the brand's identity and provides basic guidelines for color and typeface implementation.",
                        "It offers a quick and easy way for designing color palettes, assisting designers in understanding the brand and offering tips on integrating these elements into the projects."
                    ],

                    about:[
                        "The second version of the Uverit Color Palette. I wanted to build it from the ground up using TypeScript, refresh the design and add new features. The palette allows for an easy and quick way to showcase the chosen colors and typefaces.",
                        "The program is interactive to distinguish it from other brand guide and color palette services. It encourages the user to test the colors, see the implementation, and get some helpful tips on how to use everything.",
                        "I gained vast knowledge about brand presentation, color theory, as well as user interface and experience. Simplicity is the best way to present important information."
                    ],

                    stack:[
                        "HTML & CSS",
                        "JavaScript",
                        "TypeScript"
                    ]

                },

                {
                    title: "Rapid Core",
                    imgSrc: this.path('dev-projects/rapid-core-logo.svg'),

                    gitHubLink: "https://github.com/newhorizonweb/Rapid-Core",
                    pageLink: "https://newhorizonweb.github.io/Rapid-Core/",

                    mobileMockup: this.path('dev-projects/rapid-core-mobile.webp'),
                    desktopMockup: this.path('dev-projects/rapid-core-desktop.webp'),

                    overview:[
                        "Your Personal Aim Trainer",
                        "Take a deep dive into the vastness of space and test your skills in a star-worthy battle.",
                        "Rapid Core is an aim trainer that helps you improve your reaction time, aim, precision, and focus. On top of that, it lets you track your stats and discover the secrets of the most unforgettable objects in the universe."
                    ],
                    
                    about:[
                        "It was always a dream of mine to develop a game, even if it's a simple one. Rapid Core is an aim trainer with an exciting space/universe theme. It not only provides a reliable way to track one's progress, but also offers a way to have some fun while listening to an amazing soundtrack.",
                        "I chose Vue.js as the framework for the game. It's unconventional, but it allowed me to learn many things about its implementation and use. The component-based system was great for separating many parts of the program, but I also learned the cases in which this framework is not the best solution.",
                        "This project was very unique - it was something that allowed me to experience web development from a completely different side. I find it great, that many technologies not designed for some specific thing, are still flexible enough for the developer to create something inspiring."
                    ],

                    stack:[
                        "HTML & CSS",
                        "Vue.js",
                        "JavaScript",
                        "TypeScript",
                        "SASS (SCSS)"
                    ]
                    
                }

            ],



                /* Graphic Design */



            graphicDesign:[
                {
                    title: "Logos",
                    designClass: "design-row3 design-row-h",
                    scrollContent: false,
                    imgSrc: "<svg class='tile-svg1' xmlns='http://www.w3.org/2000/svg' viewBox='0 0 692 692'><defs><style></style></defs><path class='cls-2' d='M85,746a30.2,30.2,0,0,1-12.8-2.8A30.9,30.9,0,0,1,54,715V85a31,31,0,0,1,58.1-15L219,263.4a31,31,0,1,1-54.2,30L116,205.2V646.9L379.7,417.1a30.9,30.9,0,0,1,40.7,0L684,646.9V205.2l-48.7,88.2a31,31,0,0,1-54.3-30L687.9,70A31,31,0,0,1,746,85V715a31.1,31.1,0,0,1-51.4,23.4L400,481.6,105.4,738.4A31.3,31.3,0,0,1,85,746Z' transform='translate(-54 -54)'/><path class='cls-2' d='M400,686a31,31,0,0,1-27.1-16L254.3,455.4a31,31,0,1,1,54.3-29.9L400,590.9l91.4-165.4a31,31,0,1,1,54.3,29.9L427.1,670A31,31,0,0,1,400,686Z' transform='translate(-54 -54)'/><g class='anim-elem1'><path class='cls-1' d='M400,376.2a131.1,131.1,0,0,1-131-131c0-72.2,58.8-131,131-131s131,58.8,131,131A131.1,131.1,0,0,1,400,376.2Zm0-200a69,69,0,1,0,69,69A69.1,69.1,0,0,0,400,176.2Z' transform='translate(-54 -54)'/></g></svg>",

                    designs:[
                        this.path("logos/baby born.svg"),
                        this.path("logos/diamond hotel white.svg"),
                        this.path("logos/fox logo white.svg"),
                        this.path("logos/happy vet white.svg"),
                        this.path("logos/logo-wb.svg"),
                        this.path("logos/Luigi's Mansion logo excluded reverse.webp"),
                        this.path("logos/New Horizon Full white.svg"),
                        this.path("logos/rapid-core-logo.svg"),
                        this.path("logos/Superior Star Logo excluded reverse v2.webp"),
                        this.path("logos/symphony.svg"),
                        this.path("logos/timeless.svg"),
                        this.path("logos/uverit-w.svg"),
                        this.path("logos/royal-casino.svg"),
                        this.path("logos/sweet-stuff.svg"),
                        this.path("logos/My Ally.svg"),
                        this.path("logos/Cozy Fluff Logo.svg"),
                        this.path("logos/Atombits.svg"),
                        this.path("logos/jangflix.svg"),
                    ]
                },

                {
                    title: "Icons",
                    designClass: "design-row5 design-row-s",
                    scrollContent: false,
                    imgSrc: "<svg class='tile-svg2' xmlns='http://www.w3.org/2000/svg' viewBox='0 0 200 200'><g class='anim-elem1'><path class='cls-1' d='M106.5,27H120c17.4,0,31.5,14.6,31.5,30.3h0'/><path class='cls-1' d='M170.2,55.8,155.6,70.4a5.7,5.7,0,0,1-8.2,0L132.8,55.8'/></g><g class='anim-elem1'><path class='cls-1' d='M93.5,173H80c-17.4,0-31.4-14.7-31.4-30.3h0'/><path class='cls-1' d='M29.9,144.1l14.6-14.6a5.9,5.9,0,0,1,8.2,0l14.5,14.6'/></g><g class='anim-elem2 anim-elem2a'><circle class='cls-1' cx='151.5' cy='112.7' r='23'/><path class='cls-1' d='M126.3,196a22,22,0,0,1-12.2-3.6l-.7-.5c-4.2-3.1-6.4-8.3-6.8-13.3a61.4,61.4,0,0,1,.3-10.5,46.6,46.6,0,0,1,3.7-13.1,26,26,0,0,1,7.2-10.5,14.7,14.7,0,0,1,10.2-3.7c4.6.1,7.3,2.7,11.5,4.2a42.2,42.2,0,0,0,11.6,2h.3a40.9,40.9,0,0,0,11.6-2c4.2-1.5,6.9-4.1,11.5-4.2a16.6,16.6,0,0,1,10.2,3.7c3,2.3,5.6,6.6,7.3,10.5a50,50,0,0,1,3.6,13.1,61.4,61.4,0,0,1,.3,10.5c-.4,5-2.6,10.2-6.8,13.3a1.8,1.8,0,0,1-.7.5,22,22,0,0,1-12.2,3.6Z'/></g><g class='anim-elem2 anim-elem2b'><circle class='cls-1' cx='49' cy='27' r='23'/><path class='cls-1' d='M23.8,110.2a21.9,21.9,0,0,1-12.2-3.5l-.7-.6C6.7,103,4.5,97.9,4.2,92.8a52.7,52.7,0,0,1,.2-10.5,45,45,0,0,1,3.7-13c1.6-3.9,3.8-7.8,7.2-10.5A14.8,14.8,0,0,1,25.5,55c4.6.2,7.3,2.7,11.5,4.2a35.8,35.8,0,0,0,11.6,2h.3a34.9,34.9,0,0,0,11.6-2c4.2-1.5,6.9-4,11.6-4.2s7.2,1.5,10.2,3.8,5.5,6.6,7.2,10.5a48.3,48.3,0,0,1,3.6,13,61.4,61.4,0,0,1,.3,10.5,18,18,0,0,1-6.7,13.3l-.8.6a21.7,21.7,0,0,1-12.2,3.5Z'/></g></svg>",

                    designs:[
                        this.path("icons/camera-icon.svg"),
                        this.path("icons/chat-icon.svg"),
                        this.path("icons/mail-icon.svg"),
                        this.path("icons/contact-icon.svg"),

                        this.path("icons/clock-icon.svg"),
                        this.path("icons/time-icon.svg"),
                        this.path("icons/time-active-new.svg"),
                        this.path("icons/time-passive-new.svg"),
                        this.path("icons/time-total-new.svg"),

                        this.path("icons/checkmark new.svg"),
                        this.path("icons/checkmark-icon.svg"),
                        this.path("icons/do-icon.svg"),
                        this.path("icons/dont-icon.svg"),

                        this.path("icons/pin-icon.svg"),
                        this.path("icons/pin-icon2.svg"),
                        this.path("icons/upload-icon.svg"),
                        this.path("icons/settings-icon.svg"),

                        this.path("icons/phone-icon.svg"),
                        this.path("icons/mute-icon.svg"),
                        this.path("icons/website-icon.svg"),
                        this.path("icons/list-icon.svg"),
                        this.path("icons/list-icon2.svg"),
                        this.path("icons/note-icon.svg"),
                        this.path("icons/stats-icon.svg"),
                        this.path("icons/seo-icon.svg"),

                        this.path("icons/baked-goods-icon.svg"),
                        this.path("icons/dessert-icon.svg"),
                        this.path("icons/fruits-vegetables-icon.svg"),
                        this.path("icons/dish-icon.svg"),
                        this.path("icons/drink-icon.svg"),
                        this.path("icons/meat-dairy-icon.svg"),
                        this.path("icons/pastry-bag-icon.svg"),
                        this.path("icons/ready-meal-icon.svg"),
                        this.path("icons/semi-finished-products-icon.svg"),
                        this.path("icons/sweets-snacks-icon.svg"),
                        this.path("icons/snack-icon.svg"),
                        this.path("icons/spice-icon.svg"),
                        this.path("icons/grains-icon.svg"),
                        this.path("icons/other-icon.svg"),
                        this.path("icons/vegan-icon.svg"),

                        this.path("icons/recipe-icon.svg"),
                        this.path("icons/portion-number-icon.svg"),
                        this.path("icons/product-icon.svg"),
                        this.path("icons/weight-icon.svg"),
                        this.path("icons/delete-icon.svg"),

                        this.path("icons/briefcase.svg"),
                        this.path("icons/course-icon.svg"),
                        this.path("icons/color-palette-icon.svg"),
                        this.path("icons/user-icon.svg"),
                        this.path("icons/graduation-hat-icon.svg"),
                        this.path("icons/references-icon.svg"),
                        this.path("icons/dev-hero-icon.svg"),
                        this.path("icons/web-design-icon.svg"),
                        this.path("icons/light-bulb.svg"),

                        this.path("icons/pixel-art-icon.svg"),
                        this.path("icons/battery-icon.svg"),
                        this.path("icons/brush-icon.svg"),
                        this.path("icons/crosshair.svg"),
                        this.path("icons/score-icon.svg"),
                        this.path("icons/magnifying-glass-icon.svg"),
                        this.path("icons/flyer-icon.svg"),
                        this.path("icons/star.svg"),
                        this.path("icons/link new.svg"),
                        this.path("icons/turn-page-icon.svg"),

                        this.path("icons/calculator-icon.svg"),
                        this.path("icons/main-icon.svg"),
                        this.path("icons/pdf-btn.svg"),

                        this.path("icons/calendar.svg"),
                        this.path("icons/mod_calendar.svg"),
                    ]
                },

                {
                    title: "Web Design",
                    designClass: "design-row3 design-row-s",
                    scrollContent: true,
                    imgSrc: "<svg class='tile-svg3' xmlns='http://www.w3.org/2000/svg' viewBox='0 0 200 200'><rect class='cls-1' x='5.1' y='18' width='189.9' height='142.55' rx='15.7'/><line class='cls-1' x1='67.8' y1='182' x2='132.2' y2='182'/><line class='cls-1' x1='138.7' y1='138.6' x2='170.2' y2='138.6'/><line class='anim-elem4 cls-1' x1='51.6' y1='138.6' x2='116.1' y2='138.6'/><line class='cls-1' x1='29.8' y1='138.6' x2='29.9' y2='138.6'/><path class='anim-elem1 cls-2' d='M67.1,60.2l-30,17.4a1.8,1.8,0,0,0,0,3.1L67.1,98'/><path class='anim-elem3 cls-2' d='M132.9,60.2l30,17.4a1.8,1.8,0,0,1,0,3.1L132.9,98'/><line class='anim-elem2 cls-2' x1='117.5' y1='41.6' x2='82.5' y2='116.6'/></svg>",

                    designs:[
                        {
                            img: this.path("web-design/Portfolio.webp"),
                            isMobile: false
                        },
                        {
                            img: this.path("web-design/Paw Guardians.webp"),
                            isMobile: false
                        },
                        {
                            img: this.path("web-design/VibeSync.webp"),
                            isMobile: true
                        },
                        {
                            img: this.path("web-design/My Ally.webp"),
                            isMobile: true
                        },
                        {
                            img: this.path("web-design/Cozy Fluff.webp"),
                            isMobile: false
                        },
                        {
                            img: this.path("web-design/Atombits.webp"),
                            isMobile: false
                        },

                    ]
                },

                {
                    title: "Collaterals",
                    designClass: "design-row3 design-row-s",
                    scrollContent: false,
                    imgSrc: "<svg class='tile-svg4' xmlns='http://www.w3.org/2000/svg' viewBox='0 0 200 200'><path class='cls-1' d='M132,185.4V39.9'/><path class='cls-1' d='M132,36.4V190'/><path class='cls-1' d='M68,160.1V15.1'/><path class='cls-1' d='M68,163.6a11.2,11.2,0,0,1,4.4.9l53.9,24.3h0a14.1,14.1,0,0,0,11.4,0h0l56-25.2a3.8,3.8,0,0,0,2.3-3.5V14.6a4,4,0,0,0-5.7-3.5L136.4,35.5a11.2,11.2,0,0,1-4.4.9h0a11.2,11.2,0,0,1-4.4-.9L73.7,11.1h0a15,15,0,0,0-11.4,0h0L6.3,36.4A3.8,3.8,0,0,0,4,39.9V185.4a3.9,3.9,0,0,0,5.7,3.4l53.9-24.3a11.2,11.2,0,0,1,4.4-.9Z'/><path class='cls-1' d='M68,10V163.6'/></svg>",

                    designs:[
                        this.path("collaterals/DJ.webp"),
                        this.path("collaterals/uverit-flyer.webp"),
                        this.path("collaterals/aktywna-tablica.webp"),
                        this.path("collaterals/finanzexpert.webp"),
                        this.path("collaterals/m3lomoore flyer.webp"),
                        this.path("collaterals/sweet-stuff-flyer.webp"),
                        this.path("collaterals/BrianRiot.webp"),
                        this.path("collaterals/diamond hotel insert.webp"),
                        this.path("collaterals/amazon-insert1.webp"),
                        this.path("collaterals/amazon-insert2.webp"),
                        this.path("collaterals/symphony-insert.webp"),
                    ]
                },

                {
                    title: "Color Palettes",
                    designClass: "design-row3 design-row-h",
                    scrollContent: false,
                    imgSrc: "<svg class='tile-svg5' xmlns='http://www.w3.org/2000/svg' viewBox='0 0 200 200'><path class='cls-1' d='M144.4,125.4a33.4,33.4,0,0,0,5.2,1.4c7,1.4,19.6,2.7,30.4-3.5a28.7,28.7,0,0,0,7-5.5c5.4-5.6,8-13,8.8-20.7,1.1-10.5-2-21.1-6.5-30.7C175.5,37.1,146.2,14.9,114,11.2a109.5,109.5,0,0,0-46.2,4.6A101,101,0,0,0,43.4,27.9a92.4,92.4,0,0,0-26.2,27c-19.1,30-17.1,68,3.9,96.4a93.2,93.2,0,0,0,16.3,16.9c14.2,11.4,31.9,18.1,49.9,20.4a116.9,116.9,0,0,0,19.6.8c4.5-.3,9.8-.8,13.2-4.3s3.7-8.5.4-12-4.9-3.6-7.5-5.2c-9-5.5-16.2-15.7-13.2-26.6a23.3,23.3,0,0,1,10.4-12.7c3.2-1.9,9.8-4.5,19.3-4.9A45.3,45.3,0,0,1,144.4,125.4Z'/><circle class='cls-1' cx='48.6' cy='78.4' r='15.7'/><circle class='cls-1' cx='99.9' cy='49' r='15.7'/><circle class='cls-1' cx='151.6' cy='77' r='15.7'/><circle class='cls-1' cx='56.1' cy='136.9' r='15.7'/><g class='anim-elem1'><path class='cls-2' d='M138.4,119.4l53.3,53.3c4.1,4.1,4.4,10.4.7,14.1h0c-3.6,3.7-10,3.3-14.1-.7l-53.2-53.3'/><path class='cls-3' d='M120.1,92.9c6.6,3.1,10.4,5.9,13.7,11.1s7.1,17.1,0,24.1-18.6,3.4-24.1,0-8.1-7-11.2-13.7c-2.2-4.6-7.9-23.6-9.8-29.9a1.1,1.1,0,0,1,.7-1.4h.7C96.4,84.9,115.4,90.7,120.1,92.9Z'/></g></svg>",

                    designs:[
                        this.path("color-palettes/lumifilms.webp"),
                        this.path("color-palettes/Uverit Color Palette.webp"),
                        this.path("color-palettes/13-month-calendar.webp"),
                        this.path("color-palettes/akashic-resonance.webp"),
                        this.path("color-palettes/b-med.webp"),
                        this.path("color-palettes/chanan.webp"),
                        this.path("color-palettes/fireflyloop.webp"),
                        this.path("color-palettes/key-places.webp"),
                        this.path("color-palettes/mr-seo-tech.webp"),
                        this.path("color-palettes/Nursify Color Palette.webp"),
                        this.path("color-palettes/sayiastar.webp"),
                        this.path("color-palettes/sistair.webp"),
                        this.path("color-palettes/THAI GATE.webp"),
                        this.path("color-palettes/wanda-cox.webp"),
                        this.path("color-palettes/kew-central.webp"),
                        this.path("color-palettes/Amazeam.webp"),
                        this.path("color-palettes/Sincerely OMara.webp"),
                        this.path("color-palettes/Hier im Ort.webp"),
                        this.path("color-palettes/Jangflix Color Palette.webp"),
                        this.path("color-palettes/My Ally.webp"),
                        this.path("color-palettes/Cozy Fluff.webp"),
                        this.path("color-palettes/Atombits.webp"),
                        this.path("color-palettes/JoVenture.webp"),
                        this.path("color-palettes/TallSoftBoi.webp"),
                    ]
                },

                {
                    title: "Pixel Art",
                    designClass: "design-row5 design-row-s",
                    scrollContent: false,
                    imgSrc: "<svg class='tile-svg6' xmlns='http://www.w3.org/2000/svg' viewBox='0 0 200 200'><rect class='anim-elem1 cls-1' x='134.4' y='96.9' width='18.8' height='18.75'/><rect class='anim-elem1 cls-1' x='146.9' y='84.4' width='18.8' height='18.75'/><rect class='anim-elem1 cls-1' x='46.9' y='96.9' width='18.8' height='18.75'/><rect class='anim-elem1 cls-1' x='59.4' y='84.4' width='18.8' height='18.75'/><rect class='cls-1' x='37.5' y='25' width='12.5' height='12.5'/><rect class='cls-1' x='25' y='37.5' width='12.5' height='12.5'/><polygon class='cls-1' points='25 125 12.5 125 12.5 137.5 12.5 150 25 150 25 137.5 25 125'/><rect class='cls-1' x='25' y='150' width='12.5' height='12.5'/><rect class='cls-1' x='37.5' y='162.5' width='12.5' height='12.5'/><polygon class='cls-1' points='62.5 175 50 175 50 187.5 62.5 187.5 75 187.5 75 175 62.5 175'/><polygon class='cls-1' points='100 150 87.5 150 75 150 75 162.5 87.5 162.5 100 162.5 112.5 162.5 125 162.5 125 150 112.5 150 100 150'/><rect class='cls-1' x='125' y='137.5' width='12.5' height='12.5'/><rect class='cls-1' x='62.5' y='137.5' width='12.5' height='12.5'/><polygon class='cls-1' points='100 187.5 87.5 187.5 75 187.5 75 200 87.5 200 100 200 112.5 200 125 200 125 187.5 112.5 187.5 100 187.5'/><polygon class='cls-1' points='125 175 125 187.5 137.5 187.5 150 187.5 150 175 137.5 175 125 175'/><rect class='cls-1' x='150' y='162.5' width='12.5' height='12.5'/><rect class='cls-1' x='162.5' y='150' width='12.5' height='12.5'/><polygon class='cls-1' points='175 137.5 175 150 187.5 150 187.5 137.5 187.5 125 175 125 175 137.5'/><path class='cls-1' d='M187.5,75V50H175V75H25V50H12.5V75H0v50H12.5V87.5H25v25H37.5V125H75V112.5H87.5v-25h25v25H125V125h37.5V112.5H175v-25h12.5V125H200V75ZM75,100H62.5v12.5H50V100H62.5V87.5H75Zm87.5,0H150v12.5H137.5V100H150V87.5h12.5Z'/><rect class='cls-1' x='162.5' y='37.5' width='12.5' height='12.5'/><rect class='cls-1' x='150' y='25' width='12.5' height='12.5'/><polygon class='cls-1' points='137.5 25 150 25 150 12.5 137.5 12.5 125 12.5 125 25 137.5 25'/><polygon class='cls-1' points='100 12.5 112.5 12.5 125 12.5 125 0 112.5 0 100 0 87.5 0 75 0 75 12.5 87.5 12.5 100 12.5'/><polygon class='cls-1' points='75 25 75 12.5 62.5 12.5 50 12.5 50 25 62.5 25 75 25'/></svg>",

                    designs:[
                        this.path("pixel-art/rabbit.webp"),
                        this.path("pixel-art/fish1.webp"),
                        this.path("pixel-art/fish2.webp"),
                        this.path("pixel-art/fish3.webp"),

                        this.path("pixel-art/average-guy.webp"),
                        this.path("pixel-art/alien.webp"),
                        
                        this.path("pixel-art/ice-cream.webp"),
                        this.path("pixel-art/apple.webp"),
                        this.path("pixel-art/apple-golden.webp"),
                        this.path("pixel-art/beef.webp"),
                        this.path("pixel-art/beef-cooked.webp"),
                        this.path("pixel-art/bread.webp"),
                        this.path("pixel-art/carrot.webp"),
                        this.path("pixel-art/cookie.webp"),
                        this.path("pixel-art/pie.webp"),
                        this.path("pixel-art/watermelon.webp"),
                        this.path("pixel-art/toadstool.webp"),
                        this.path("pixel-art/mushroom.webp"),

                        this.path("pixel-art/pickaxe.webp"),
                        this.path("pixel-art/axe.webp"),
                        this.path("pixel-art/shovel.webp"),
                        this.path("pixel-art/sword.webp"),
                        this.path("pixel-art/hoe.webp"),

                        this.path("pixel-art/iron helmet.webp"),
                        this.path("pixel-art/iron chestplate.webp"),
                        this.path("pixel-art/iron trousers.webp"),
                        this.path("pixel-art/iron boots.webp"),

                        this.path("pixel-art/golden helmet.webp"),
                        this.path("pixel-art/golden chestplate.webp"),
                        this.path("pixel-art/golden trousers.webp"),
                        this.path("pixel-art/golden boots.webp"),

                        this.path("pixel-art/iron ingot.webp"),
                        this.path("pixel-art/gold ingot.webp"),
                        this.path("pixel-art/coin.webp"),

                        this.path("pixel-art/bomb.webp"),
                        this.path("pixel-art/bone.webp"),
                        this.path("pixel-art/egg.webp"),
                    ]
                }

            ],



                /* Code */
                    
                    

            // Prop Components (raw = no reactivity)
            ProjectModal: markRaw(ProjectModal),
            DesignModal: markRaw(DesignModal),

            // Sections
            mainSections: document.querySelectorAll(".main-section"),
            wasSectionLoaded: {} as { [key: string]: boolean },

            // Observer
            observer: null as IntersectionObserver | null,

            options: {
                root: null, // Use the viewport as the root
                rootMargin: '50px', // Margin
                threshold: 0, // How much of the element should be visible (0.5 = 50%)
            }

        }
    },

    mounted(){

            /* Section Visibility Observation */

        // Create the IntersectionObserver
        this.observer = new IntersectionObserver(this.sectionIntersection, this.options);

        // Set the sections
        this.mainSections = document.querySelectorAll(".main-section");

        // Initialize the observer
        this.observeSections();

        // Disable the fade-in/out animation on mobile (performance improvement)
        window.addEventListener("resize", this.sectionsOnResize);

        // Load the sections on click (anywhere) - nav links fix
        window.addEventListener("click", this.loadComponents);

    },

    methods:{

            /* Section Observer */

        loadComponents(){

            this.mainSections.forEach((section: Element) => {
                this.wasSectionLoaded[section.id] = true;
            });

        },

        observeSections(){

            this.mainSections.forEach((section: Element) => {

                this.wasSectionLoaded[section.id] = false;

                if (this.observer){
                    this.observer.observe(section);
                }

            });

            this.sectionsOnResize();

        },

        sectionsOnResize(){

            this.mainSections.forEach((section: Element) => {

                // Check if the section is above the page view
                const isAboveView = section.getBoundingClientRect().top >= window.innerHeight;

                if (window.innerWidth > 768 && isAboveView){
                    section.classList.add("section-out");
                } else {
                    section.classList.remove("section-out");
                }

            });

        },

        sectionIntersection(entries: IntersectionObserverEntry[]){

            entries.forEach((entry: IntersectionObserverEntry) => {

                const section = entry.target;
                const sectionId = section.id;
                const isAbove = entry.boundingClientRect.top >= 0;
                
                // Check if the user is scrolled past the section
                if (entry.isIntersecting){

                    this.wasSectionLoaded[sectionId] = true;
                    section.classList.remove("section-out");

                } else if (isAbove && window.innerWidth > 768){

                    section.classList.add("section-out");

                }

            });

        },

            /* Image Path */

        path(imgName: string){
            return require("@/assets/img/" + imgName);
        }
        
    }

});
</script>



<style lang="scss">

main{
    padding-top:calc(
        (var(--size6) + var(--size5) * 2) + 
        var(--size7) + var(--size8)
    );
    position:relative;

    display:flex;
    flex-direction:column;
    gap:calc(var(--size8) * 2.5);
    z-index:110;

    & .section-heading{
        width:100%;
        font-size:min(34px, 6vw);
        text-align:center;
    }

    & .tile-heading-capital{
        text-transform:capitalize;
    }

        /* Main Section */

    .main-section{
        position:relative;
        top:0;
        transition:1s ease-out;

        &:not(:has(.tile-modal-open)).section-out{
            top:150px;
            opacity:0;
            filter:brightness(75%);
        }

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