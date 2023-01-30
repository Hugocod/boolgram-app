<template>
    <div class="container">
        <sidebar-section :navLinks="navLinks"></sidebar-section>
    </div>
</template>

<script>
import SidebarSection from "../secondary/SidebarSection/SidebarSection.vue";
export default {
    components: { SidebarSection },
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

            apiProfiles: "https://flynn.boolean.careers/exercises/api/boolgram/profiles",
            apiPost: "https://flynn.boolean.careers/exercises/api/boolgram/posts",
        };
    },
};
</script>

<style lang="scss" scoped>
.container {
    height: 100vh;
    background-color: #beb7b7;

    display: flex;
}
</style>
