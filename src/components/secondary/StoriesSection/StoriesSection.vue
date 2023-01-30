<template>
    <div class="stories-container">
        <swiper
            :spaceBetween="10"
            :slidesPerView="calculateSlidesNumber"
            :pagination="false"
            :navigation="false"
            :modules="modules"
            class="mySwiper">
            <swiper-slide
                v-for="(profile, index) in profilesData.data"
                :key="index">
                <div class="story-thumb">
                    <img :src="profile.profile_picture" />
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
    width: 27rem;

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

    outline: 3px solid red;
    outline-offset: 3px;
}

.story-thumb {
    padding: 0.7rem;

    .name-container {
        overflow: hidden;
        white-space: nowrap;

        text-overflow: ellipsis;

        a {
            color: red($color: #000000);
        }
    }
}
</style>
