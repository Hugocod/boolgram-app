<template>
    <div class="stories-container">
        <swiper
            :spaceBetween="10"
            :autoplay="true"
            :delay="1"
            :pauseOnMouseEnter="false"
            :slidesPerView="calculateSlidesNumber"
            :pagination="false"
            :navigation="fasle"
            :modules="modules"
            class="mySwiper">
            <swiper-slide
                v-for="(profile, index) in profilesData.data"
                :key="index">
                <div class="story-thumb">
                    <div class="gradient-circle">
                        <img :src="profile.profile_picture" />
                    </div>
                    <div class="name-container">
                        <a>{{ profile.profile_name }}</a>
                    </div>
                </div>
            </swiper-slide>
        </swiper>
    </div>
</template>
<script>
// Import Swiper Vue.js components
import { Swiper, SwiperSlide } from "swiper/vue";

// Import Swiper styles
import "swiper/css";

// import required modules
import { Autoplay, Pagination, Navigation } from "swiper";

export default {
    name: "StoriesComponent",
    components: {
        Swiper,
        SwiperSlide,
    },
    props: {
        /* dati del post ricevuti via props (la chiamata API è nel parent); */
        profilesData: Object,
    },
    data() {
        return {
            numberOfSlides: "5",
            width: "",
        };
    },
    setup() {
        return {
            modules: [Autoplay, Pagination, Navigation],
        };
    },
    //
    mounted() {
        this.width = window.innerWidth;
        window.addEventListener("resize", this.handleResize);
    },
    //
    beforeUnmount() {
        window.removeEventListener("resize", this.handleResize);
    },
    //
    methods: {
        handleResize() {
            this.width = window.innerWidth;
        },
    },
    //
    computed: {
        calculateSlidesNumber() {
            if (this.width > 660) {
                return 5;
            } else if (this.width < 470) {
                return 3;
            } else {
                return 4;
            }
        },
    },
};
</script>

<style scoped lang="scss">
/* @import "../../../scss/resources"; */

.stories-container {
    width: 29rem;

    @media (max-width: 470px) {
        width: 20rem;
    }

    @media (max-width: 340px) {
        width: 18rem;
    }

    background-color: white;
    border-radius: 0.5rem;

    padding: 0.7rem;

    border: 0.09rem solid rgb(215, 209, 209);

    text-align: center;
}
img {
    border-radius: 50%;
    width: 100%;
    aspect-ratio: 4 / 4;

    border: 2.7px solid white;
}

.story-thumb {
    padding: 0.2rem;

    .gradient-circle {
        background-color: aqua;
        padding: 0.2rem;
        border-radius: 50%;

        display: flex;
        justify-content: center;
        align-items: center;

        /*  instagram gradient */
        background: -webkit-radial-gradient(
                32% 106%,
                circle cover,
                rgb(255, 225, 125) 0%,
                rgb(255, 205, 105) 10%,
                rgb(250, 145, 55) 28%,
                rgb(235, 65, 65) 42%,
                transparent 82%
            ),
            -webkit-linear-gradient(-45deg, rgb(35, 75, 215) 12%, rgb(
                            195,
                            60,
                            190
                        )
                        58%);
        background: -moz-radial-gradient(
                32% 106%,
                circle cover,
                rgb(255, 225, 125) 0%,
                rgb(255, 205, 105) 10%,
                rgb(250, 145, 55) 28%,
                rgb(235, 65, 65) 42%,
                transparent 82%
            ),
            -moz-linear-gradient(-45deg, rgb(35, 75, 215) 12%, rgb(195, 60, 190)
                        58%);
        background: -ms-radial-gradient(
                32% 106%,
                circle cover,
                rgb(255, 225, 125) 0%,
                rgb(255, 205, 105) 10%,
                rgb(250, 145, 55) 28%,
                rgb(235, 65, 65) 42%,
                transparent 82%
            ),
            -ms-linear-gradient(-45deg, rgb(35, 75, 215) 12%, rgb(195, 60, 190)
                        58%);
        background: -o-radial-gradient(
                32% 106%,
                circle cover,
                rgb(255, 225, 125) 0%,
                rgb(255, 205, 105) 10%,
                rgb(250, 145, 55) 28%,
                rgb(235, 65, 65) 42%,
                transparent 82%
            ),
            -o-linear-gradient(-45deg, rgb(35, 75, 215) 12%, rgb(195, 60, 190)
                        58%);
        background: radial-gradient(
                circle farthest-corner at 32% 106%,
                rgb(255, 225, 125) 0%,
                rgb(255, 205, 105) 10%,
                rgb(250, 145, 55) 28%,
                rgb(235, 65, 65) 42%,
                transparent 82%
            ),
            linear-gradient(135deg, rgb(35, 75, 215) 12%, rgb(195, 60, 190) 58%);
    }

    .name-container {
        overflow: hidden;
        white-space: nowrap;

        text-overflow: ellipsis;

        a {
            color: red($color: #000000);
            font-weight: 500;
            font-size: 0.9rem;
            color: black;
        }
    }
}
</style>
