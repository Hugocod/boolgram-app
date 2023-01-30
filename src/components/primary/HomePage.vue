<template>
    <div class="container-home">
        <sidebar-section :navLinks="navLinks"></sidebar-section>

        <feed-section v-if="posts.isDataLoaded" :postData="posts.data">
        </feed-section>
    </div>
</template>

<script>
import FeedSection from "../secondary/FeedSection/FeedSection.vue";
import SidebarSection from "../secondary/SidebarSection/SidebarSection.vue";

import axios from "axios";
export default {
    components: { SidebarSection, FeedSection },
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
        /*  setTimeout(() => {
            this.getData(this.apiPost, this.posts);
            this.getData(this.apiProfiles, this.profiles);
        }, 1000); */

        this.getData(this.apiPost, this.posts);
        this.getData(this.apiProfiles, this.profiles);
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
.container-home {
    height: 100vh;
    /* background-color: #beb7b7; */

    display: flex;
}
</style>
