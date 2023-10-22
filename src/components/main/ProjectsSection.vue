


<template>

    <div id="dev-projects" class="dev-projects wrapper">

        <h2 class="section-heading"
            data-text="Web-Dev Projects">
        </h2>

        <div class="project-tile glass-tile"
            ref="projectTile"

            v-for="project in projects" 
            :key="project.title">

            <ProjectModal
                :data="project"
                @hideModals="hideModals"
            />

        </div>

    </div>

</template>



<script lang="ts">
import { defineComponent } from 'vue';
import ProjectModal from "./ProjectModal.vue";

interface Project{
    logo: string;
    title: string;

    mobileMockup: string;
    desktopMockup: string;

    overview: string[];
    about: string[];
    stack: string[];
}

export default defineComponent({
    name: "ProjectsSection",

    components:{
        ProjectModal
    },

    data(){
        return{

            // Project Data
            projects:[

                {
                    title: "Cookbook",
                    logoSrc: this.path('uverit-logo.svg'),
                    
                    mobileMockup: this.path('cookbook-mobile.png'),
                    desktopMockup: this.path('cookbook-desktop.png'),

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
                    logoSrc: this.path('uverit-logo.svg'),

                    mobileMockup: this.path('logo-test-mobile.png'),
                    desktopMockup: this.path('logo-test-desktop.png'),

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
                    logoSrc: this.path('uverit-logo.svg'),

                    mobileMockup: this.path('skillpeak-mobile.png'),
                    desktopMockup: this.path('skillpeak-desktop.png'),

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
                    logoSrc: this.path('uverit-logo.svg'),

                    mobileMockup: this.path('color-palette-mobile.png'),
                    desktopMockup: this.path('color-palette-desktop.png'),

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
                    logoSrc: this.path('rapid-core-logo.svg'),

                    mobileMockup: this.path('rapid-core-mobile.png'),
                    desktopMockup: this.path('rapid-core-desktop.png'),

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

            // Modal
            currProjTile: null as null | HTMLElement

        } 
    },

    mounted(){

        // Add the tile click events
        this.tileModal();

        // Modal placement on resize
        let resizeTimer: number;

        window.addEventListener("resize", () => {

            clearTimeout(resizeTimer);

            if (this.currProjTile &&
            this.currProjTile.classList.contains("tile-modal")){

                this.currTilePos(this.currProjTile);

                // Ensure the correct placement
                // Sometimes the resize event dwould not be registered correctly
                resizeTimer = setTimeout(() => {
                    this.currTilePos(this.currProjTile!);
                }, 400);

            }

        });

    },

    methods:{

            /* Base Function Elements */

        path(imgName: string){
            return require("@/assets/img/modals/" + imgName);
        },

        hideModals(currTile?: HTMLElement){

            // Disable the modal mode
            document.documentElement.classList.remove("modal-mode");

            const tiles = this.$refs.projectTile as HTMLElement[];

            tiles.forEach((tile) => {

                (tile.querySelector(".project-modal") as HTMLElement)!.style.transform = "translate3d(0px, 0px, 0px)";
                    
                tile.classList.remove("tile-modal");
                tile.classList.remove("no-trans");

                if (tile !== currTile){
                    setTimeout(() => {
                        tile.classList.remove("modal-opacity");
                    }, 500);
                }

            });

        },

        currTilePos(tile: HTMLElement){

            // Get the tile position
            const rect = tile.getBoundingClientRect();
            const transX = -rect.left;
            const transY = -rect.top;

            // Set the transform property (position modal in the center)
            (tile.querySelector(".project-modal") as HTMLElement)!.style.transform = 
                `translate3d(${transX}px, ${transY}px, 0px)`;

        },

            /* Doing Stuff */

        tileModal(){

            const tiles = this.$refs.projectTile as HTMLElement[];

            tiles.forEach((tile) => {
                tile.addEventListener("click", (e: Event) => {

                    if (e.target === tile){

                        // Hide the other modals
                        this.hideModals(tile);

                        // Set the page to the modal mode
                        document.documentElement.classList.add("modal-mode");

                        // Set the current modal tile
                        this.currProjTile = tile;

                        // Adjust the modal position
                        this.currTilePos(tile);

                        // Show modal
                        tile.classList.add("tile-modal");
                        tile.classList.add("modal-opacity");

                        // Remove the transition effect after the modal has covered the page
                        setTimeout(() => {
                            tile.classList.add("no-trans");
                        }, 750);

                    }

                });
            });

        }

    }

});
</script>



<style lang="scss">

.modal-mode{
    overflow:hidden;
}

.dev-projects{
    display:flex;
    position:relative;
    flex-wrap:wrap;
    gap:var(--size8);

    &:has(.tile-modal){
        z-index:11000;
    }

        /* Tile */

    & .project-tile{
        width:calc(50% - (var(--size8) / 2));
        height:300px;
        position:relative;

        box-shadow:inset 0 0 0 0 transparent;
        cursor:pointer;

        &:nth-last-of-type(1){
            width:100%; /* If the number of tiles is odd */
        }

        &.tile-modal{
            z-index:11000;
            cursor:auto;
        }

        &.modal-opacity{
            z-index:50;
        }

        &:hover{
            box-shadow:inset 0 0 max(5vw, 50px) 1px rgba(222, 183, 255, 0.25);
        }

    }

}

@media screen and (width <= 540px){

    .dev-projects{

        & .project-tile{
            width:100%;
            height:275px;
        }

    }

}

</style>