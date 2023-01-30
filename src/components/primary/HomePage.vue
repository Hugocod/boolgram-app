<template>
    <div class="container-home">
        <sidebar-section :navLinks="navLinks"></sidebar-section>

        <div class="main-content">
            <feed-section :postData="posts" :profilesData="profiles">
            </feed-section>
            <suggested-section :profilesData="profiles"> </suggested-section>

            <!-- Viene mostrato su mobile -->
            <div class="mobile-header">
                <img src="@/assets/boolgram-asset/logoDesktop.svg" />

                <div class="input-container">
                    <font-awesome-icon icon="fa-regular fa-heart icon" />
                </div>
            </div>

            <!-- Viene mostrato su mobile -->
            <div class="mobile-sidebar">
                <font-awesome-icon
                    v-for="(navLink, index) in navLinks.slice(0, 4)"
                    :key="index"
                    :icon="navLink.icon" />
            </div>
        </div>
    </div>
</template>

<script>
import FeedSection from "../secondary/FeedSection/FeedSection.vue";
import SidebarSection from "../secondary/SidebarSection/SidebarSection.vue";
import SuggestedSection from "../secondary/SuggestedSection/SuggestedSection.vue";

import axios from "axios";
export default {
    components: { SidebarSection, FeedSection, SuggestedSection },
    name: "HomePage",
    data() {
        return {
            // data è destinata a contenere i dati recuperati dall'API,
            // isDataloaded indica se sono stati caricati
            posts: { data: "", isDataLoaded: false },
            profiles: { data: "", isDataLoaded: false },

            navLinks: [
                { text: "home", icon: "fa-solid fa-house icon" },
                { text: "cerca", icon: "fa-solid fa-magnifying-glass icon" },
                { text: "esplora", icon: "fa-regular fa-compass icon" },
                { text: "messaggi", icon: "fa-regular fa-paper-plane icon" },
                { text: "notifiche", icon: "fa-regular fa-heart icon" },
                { text: "aggiungi", icon: "fa-regular fa-square-plus icon" },
            ],

            apiProfiles:
                "https://flynn.boolean.careers/exercises/api/boolgram/profiles",
            apiPost:
                "https://flynn.boolean.careers/exercises/api/boolgram/posts",
        };
    },
    mounted() {
        //chiamate api

        /* simula il ritardo */
        setTimeout(() => {
            this.getData(this.apiPost, this.posts);
            this.getData(this.apiProfiles, this.profiles);
        }, 3000);

        /*  this.getData(this.apiPost, this.posts);
        this.getData(this.apiProfiles, this.profiles); */
    },
    //
    methods: {
        // La seguente funzione accetta come parametri:
        //- url dell'endpoint
        //- variabile in cui finiscono i dati
        getData(url, dataContainer) {
            axios
                .get(url)
                .then((response) => {
                    console.log(response.data);
                    dataContainer.data = response.data;
                    dataContainer.isDataLoaded = true;
                })
                .catch((error) => {
                    console.log(error);
                });
        },
    },
};
</script>

<style lang="scss" scoped>
@import "../../scss/resources";

.container-home {
    height: 100vh;

    width: auto;
    position: relative;

    display: flex;
    justify-content: center;
    align-items: center;

    .main-content {
        /* position: fixed;
        top: 0;
        right: 0; */

        display: flex;
        justify-content: center;

        background-color: $color-gray-light;

        width: 100%;
        height: 100vh;
        overflow-y: scroll;
        overflow-x: hidden;

        @media (max-width: 768px) {
            padding: 4rem 0rem;
        }

        .mobile-header {
            width: 100%;
            position: fixed;
            top: 0;
            right: 0;
            height: 4rem;
            background-color: white;

            border-bottom: 0.09rem solid rgb(215, 209, 209);

            padding: 0.7rem 1.5rem;

            display: flex;
            justify-content: space-between;

            z-index: 10;

            .input-container {
                height: 100%;
                display: flex;
                justify-content: center;
                align-items: center;

                .fa-heart {
                    font-size: 1.6rem;
                    color: black;
                }
            }

            @media (min-width: 768px) {
                display: none;
            }
        }

        .mobile-sidebar {
            width: 100%;
            position: fixed;
            bottom: 0;
            right: 0;
            height: 3.4rem;
            align-items: center;
            background-color: white;

            border-top: 0.09rem solid rgb(215, 209, 209);

            display: flex;
            justify-content: space-around;

            z-index: 10;

            .fa-house,
            .fa-paper-plane,
            .fa-magnifying-glass,
            .fa-compass {
                font-size: 1.5rem;
            }

            @media (min-width: 768px) {
                display: none;
            }
        }
    }
}
</style>
