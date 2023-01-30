<template>
    <div class="stories-container">
        <swiper
            :spaceBetween="10"
            :slidesPerView="5"
            :pagination="false"
            :navigation="true"
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

import "swiper/css/pagination";
import "swiper/css/navigation";

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
        return {};
    },
    setup() {
        return {
            modules: [Autoplay, Pagination, Navigation],
        };
    },
    mounted() {
        console.log(this.profilesData);
    },
};
</script>

<style scoped lang="scss">
.stories-container {
    width: 30rem;
    margin: auto 0;

    background-color: white;
    border-radius: 0.5rem;
    border: 0.05rem solid gray;

    padding: 0.7rem;

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
