


<template>

    <main>

        <AboutSection />

        <!-- Dev Projects -->

        <TilesSection
            :modalComp="ProjectModal"
            :contents="devProjects"

            sectionTitle="Web-Dev Projects"
        />

        <!-- Graphic Design -->

        <TilesSection
            :modalComp="DesignModal"
            :contents="graphicDesign"

            sectionTitle="Graphic Design"
        />

    </main>

</template>



<script lang="ts">
import { defineComponent, markRaw } from 'vue';
import AboutSection from "./AboutSection.vue";
import TilesSection from "./TilesSection.vue";

import ProjectModal from "./ProjectModal.vue";
import DesignModal from "./DesignModal.vue";

export default defineComponent({
    name: "MainSection",

    components:{
        AboutSection,
        TilesSection
    },

    data(){
        return{
            
            // Prop Components (raw = no reactivity)
            ProjectModal: markRaw(ProjectModal),
            DesignModal: markRaw(DesignModal),

            // Dev Projects
            devProjects:[

                {
                    title: "Cookbook",
                    imgSrc: this.path('projects/uverit-logo.svg'),
                    
                    mobileMockup: this.path('projects/cookbook-mobile.png'),
                    desktopMockup: this.path('projects/cookbook-desktop.png'),

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
                    imgSrc: this.path('projects/uverit-logo.svg'),

                    mobileMockup: this.path('projects/logo-test-mobile.png'),
                    desktopMockup: this.path('projects/logo-test-desktop.png'),

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
                    imgSrc: this.path('projects/uverit-logo.svg'),

                    mobileMockup: this.path('projects/skillpeak-mobile.png'),
                    desktopMockup: this.path('projects/skillpeak-desktop.png'),

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
                    imgSrc: this.path('projects/uverit-logo.svg'),

                    mobileMockup: this.path('projects/color-palette-mobile.png'),
                    desktopMockup: this.path('projects/color-palette-desktop.png'),

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
                    imgSrc: this.path('projects/rapid-core-logo.svg'),

                    mobileMockup: this.path('projects/rapid-core-mobile.png'),
                    desktopMockup: this.path('projects/rapid-core-desktop.png'),

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

            graphicDesign:[
                {
                    title: "Logos",
                    designClass: "design-row3 design-row-h",
                    imgSrc: "<svg class='tile-svg1' xmlns='http://www.w3.org/2000/svg' viewBox='0 0 692 692'><defs><style></style></defs><path class='cls-2' d='M85,746a30.2,30.2,0,0,1-12.8-2.8A30.9,30.9,0,0,1,54,715V85a31,31,0,0,1,58.1-15L219,263.4a31,31,0,1,1-54.2,30L116,205.2V646.9L379.7,417.1a30.9,30.9,0,0,1,40.7,0L684,646.9V205.2l-48.7,88.2a31,31,0,0,1-54.3-30L687.9,70A31,31,0,0,1,746,85V715a31.1,31.1,0,0,1-51.4,23.4L400,481.6,105.4,738.4A31.3,31.3,0,0,1,85,746Z' transform='translate(-54 -54)'/><path class='cls-2' d='M400,686a31,31,0,0,1-27.1-16L254.3,455.4a31,31,0,1,1,54.3-29.9L400,590.9l91.4-165.4a31,31,0,1,1,54.3,29.9L427.1,670A31,31,0,0,1,400,686Z' transform='translate(-54 -54)'/><g class='anim-elem1'><path class='cls-1' d='M400,376.2a131.1,131.1,0,0,1-131-131c0-72.2,58.8-131,131-131s131,58.8,131,131A131.1,131.1,0,0,1,400,376.2Zm0-200a69,69,0,1,0,69,69A69.1,69.1,0,0,0,400,176.2Z' transform='translate(-54 -54)'/></g></svg>",

                    designs:[
                        this.path("color-palettes/tripod.png"),
                        this.path("color-palettes/sewing-kit.jpg"),
                        this.path("color-palettes/sewing-kit.jpg"),
                        this.path("color-palettes/tripod.png"),
                        this.path("color-palettes/tripod.png"),
                    ]
                },

                {
                    title: "Icons",
                    designClass: "design-row5 design-row-s",
                    imgSrc: "<svg class='tile-svg2' data-name='Layer 1' xmlns='http://www.w3.org/2000/svg' viewBox='0 0 200 200'><g class='anim-elem1'><path class='cls-1' d='M106.5,27H120c17.4,0,31.5,14.6,31.5,30.3h0'/><path class='cls-1' d='M170.2,55.8,155.6,70.4a5.7,5.7,0,0,1-8.2,0L132.8,55.8'/></g><g class='anim-elem1'><path class='cls-1' d='M93.5,173H80c-17.4,0-31.4-14.7-31.4-30.3h0'/><path class='cls-1' d='M29.9,144.1l14.6-14.6a5.9,5.9,0,0,1,8.2,0l14.5,14.6'/></g><g class='anim-elem2 anim-elem2a'><circle class='cls-1' cx='151.5' cy='112.7' r='23'/><path class='cls-1' d='M126.3,196a22,22,0,0,1-12.2-3.6l-.7-.5c-4.2-3.1-6.4-8.3-6.8-13.3a61.4,61.4,0,0,1,.3-10.5,46.6,46.6,0,0,1,3.7-13.1,26,26,0,0,1,7.2-10.5,14.7,14.7,0,0,1,10.2-3.7c4.6.1,7.3,2.7,11.5,4.2a42.2,42.2,0,0,0,11.6,2h.3a40.9,40.9,0,0,0,11.6-2c4.2-1.5,6.9-4.1,11.5-4.2a16.6,16.6,0,0,1,10.2,3.7c3,2.3,5.6,6.6,7.3,10.5a50,50,0,0,1,3.6,13.1,61.4,61.4,0,0,1,.3,10.5c-.4,5-2.6,10.2-6.8,13.3a1.8,1.8,0,0,1-.7.5,22,22,0,0,1-12.2,3.6Z'/></g><g class='anim-elem2 anim-elem2b'><circle class='cls-1' cx='49' cy='27' r='23'/><path class='cls-1' d='M23.8,110.2a21.9,21.9,0,0,1-12.2-3.5l-.7-.6C6.7,103,4.5,97.9,4.2,92.8a52.7,52.7,0,0,1,.2-10.5,45,45,0,0,1,3.7-13c1.6-3.9,3.8-7.8,7.2-10.5A14.8,14.8,0,0,1,25.5,55c4.6.2,7.3,2.7,11.5,4.2a35.8,35.8,0,0,0,11.6,2h.3a34.9,34.9,0,0,0,11.6-2c4.2-1.5,6.9-4,11.6-4.2s7.2,1.5,10.2,3.8,5.5,6.6,7.2,10.5a48.3,48.3,0,0,1,3.6,13,61.4,61.4,0,0,1,.3,10.5,18,18,0,0,1-6.7,13.3l-.8.6a21.7,21.7,0,0,1-12.2,3.5Z'/></g></svg>",

                    designs:[
                        this.path("icons/github-icon.svg"),
                        this.path("icons/seo-icon.svg"),
                        this.path("icons/flyer-icon.svg"),
                        this.path("icons/linkedin-icon.svg"),
                        this.path("icons/seo-icon.svg"),
                        this.path("icons/linkedin-icon.svg"),
                        this.path("icons/flyer-icon.svg"),
                        this.path("icons/github-icon.svg"),
                        this.path("icons/seo-icon.svg"),
                        this.path("icons/flyer-icon.svg"),
                        this.path("icons/flyer-icon.svg"),
                        this.path("icons/github-icon.svg"),
                        this.path("icons/seo-icon.svg"),
                        this.path("icons/flyer-icon.svg"),
                        this.path("icons/linkedin-icon.svg"),
                        this.path("icons/seo-icon.svg"),
                        this.path("icons/github-icon.svg"),
                        this.path("icons/github-icon.svg"),
                        this.path("icons/linkedin-icon.svg"),
                        this.path("icons/linkedin-icon.svg"),
                        this.path("icons/seo-icon.svg"),
                        this.path("icons/github-icon.svg"),
                        this.path("icons/linkedin-icon.svg"),
                        this.path("icons/flyer-icon.svg"),
                    ]
                },

                {
                    title: "Flyers",
                    designClass: "design-row3 design-row-s",
                    imgSrc: "<svg class='tile-svg3' data-name='Layer 1' xmlns='http://www.w3.org/2000/svg' viewBox='0 0 200 200'><path class='cls-1' d='M52,13.3V168.4'/><path class='cls-1' d='M100,186.7V31.6'/><path class='cls-1' d='M100,31.6V186.7'/><path class='cls-1' d='M52,168.4V13.3'/><path class='cls-1' d='M148,168.4V13.3'/><path class='cls-1' d='M152.5,173.1l37.4,17.1a4.3,4.3,0,0,0,6.1-3.9V31.8a4.5,4.5,0,0,0-2.5-4L159,12a27.5,27.5,0,0,0-11-2.4h0A27.5,27.5,0,0,0,137,12L104.5,26.9a9.9,9.9,0,0,1-4.5,1h0a9.9,9.9,0,0,1-4.5-1L63,12A27.5,27.5,0,0,0,52,9.6h0A27.5,27.5,0,0,0,41,12L6.5,27.8a4.5,4.5,0,0,0-2.5,4V186.3a4.3,4.3,0,0,0,6.1,3.9l37.4-17.1a9.9,9.9,0,0,1,4.5-1h0a9.9,9.9,0,0,1,4.5,1L89,188a27.5,27.5,0,0,0,11,2.4h0a27.5,27.5,0,0,0,11-2.4l32.5-14.9a9.9,9.9,0,0,1,4.5-1h0A9.9,9.9,0,0,1,152.5,173.1Z'/><path class='cls-1' d='M148,13.3V168.4'/></svg>",

                    designs:[
                        this.path("color-palettes/tripod.png"),
                        this.path("color-palettes/sewing-kit.jpg"),
                        this.path("color-palettes/sewing-kit.jpg"),
                        this.path("color-palettes/tripod.png"),
                        this.path("color-palettes/tripod.png"),
                    ]
                },

                {
                    title: "Color Palettes",
                    designClass: "design-row3 design-row-h",
                    imgSrc: "<svg class='tile-svg4' data-name='Layer 1' xmlns='http://www.w3.org/2000/svg' viewBox='0 0 200 200'><path class='cls-1' d='M144.4,125.4a33.4,33.4,0,0,0,5.2,1.4c7,1.4,19.6,2.7,30.4-3.5a28.7,28.7,0,0,0,7-5.5c5.4-5.6,8-13,8.8-20.7,1.1-10.5-2-21.1-6.5-30.7C175.5,37.1,146.2,14.9,114,11.2a109.5,109.5,0,0,0-46.2,4.6A101,101,0,0,0,43.4,27.9a92.4,92.4,0,0,0-26.2,27c-19.1,30-17.1,68,3.9,96.4a93.2,93.2,0,0,0,16.3,16.9c14.2,11.4,31.9,18.1,49.9,20.4a116.9,116.9,0,0,0,19.6.8c4.5-.3,9.8-.8,13.2-4.3s3.7-8.5.4-12-4.9-3.6-7.5-5.2c-9-5.5-16.2-15.7-13.2-26.6a23.3,23.3,0,0,1,10.4-12.7c3.2-1.9,9.8-4.5,19.3-4.9A45.3,45.3,0,0,1,144.4,125.4Z'/><circle class='cls-1' cx='48.6' cy='78.4' r='15.7'/><circle class='cls-1' cx='99.9' cy='49' r='15.7'/><circle class='cls-1' cx='151.6' cy='77' r='15.7'/><circle class='cls-1' cx='56.1' cy='136.9' r='15.7'/><g class='anim-elem1'><path class='cls-2' d='M138.4,119.4l53.3,53.3c4.1,4.1,4.4,10.4.7,14.1h0c-3.6,3.7-10,3.3-14.1-.7l-53.2-53.3'/><path class='cls-3' d='M120.1,92.9c6.6,3.1,10.4,5.9,13.7,11.1s7.1,17.1,0,24.1-18.6,3.4-24.1,0-8.1-7-11.2-13.7c-2.2-4.6-7.9-23.6-9.8-29.9a1.1,1.1,0,0,1,.7-1.4h.7C96.4,84.9,115.4,90.7,120.1,92.9Z'/></g></svg>",

                    designs:[
                        this.path("color-palettes/tripod.png"),
                        this.path("color-palettes/sewing-kit.jpg"),
                        this.path("color-palettes/tripod.png"),
                        this.path("color-palettes/tripod.png"),
                        this.path("color-palettes/sewing-kit.jpg"),
                        this.path("color-palettes/sewing-kit.jpg"),
                        this.path("color-palettes/tripod.png"),
                        this.path("color-palettes/sewing-kit.jpg"),
                        this.path("color-palettes/sewing-kit.jpg"),
                        this.path("color-palettes/tripod.png"),
                        this.path("color-palettes/tripod.png"),
                        this.path("color-palettes/tripod.png"),
                        this.path("color-palettes/sewing-kit.jpg"),
                    ]
                },
            ]

        }
    },

    methods:{

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