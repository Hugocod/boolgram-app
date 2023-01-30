<template>
    <!--  La barra laterale visualizza un logo e una serie di link di navigazione, che vengono generati dinamicamente dalla proprietà "navLinks". Ciascun link è rappresentato da un'icona e un testo,
    entrambi specificati tramite slot. -->
    <div class="sidebar-container">
        <div>
            <div class="logo-mobile" v-if="width < 1264">
                <img src="@/assets/boolgram-asset/logoMobile.svg" />
            </div>
            <img
                class="logo-desktop"
                v-else
                src="@/assets/boolgram-asset/logoDesktop.svg" />

            <div>
                <nav-link v-for="(navLink, index) in navLinks" :key="index">
                    <template v-slot:icon>
                        <font-awesome-icon :icon="navLink.icon" />
                    </template>

                    <template v-slot:text>
                        <a>{{ navLink.text }}</a>
                    </template>
                </nav-link>
            </div>
        </div>

        <nav-link>
            <template v-slot:icon>
                <font-awesome-icon icon="fa-solid fa-bars icon" />
            </template>

            <template v-slot:text>
                <a>altro</a>
            </template>
        </nav-link>
    </div>
</template>

<script>
import NavLink from "./NavLink.vue";
export default {
    name: "SidebarSection",

    data() {
        return {
            width: "",
        };
    },
    props: {
        navLinks: Array,
    },
    components: { NavLink },
    //
    mounted() {
        this.width = window.innerWidth;
        window.addEventListener("resize", this.handleResize);
    },
    beforeUnmount() {
        window.removeEventListener("resize", this.handleResize);
    },
    methods: {
        handleResize() {
            this.width = window.innerWidth;
        },
    },
};
</script>

<style lang="scss" scoped>
.sidebar-container {
    height: 100vh;
    width: fit-content;
    background-color: rgb(184, 32, 32);

    display: flex;
    flex-direction: column;
    justify-content: space-between;

    border-right: 0.05rem solid rgb(197, 189, 189);

    .logo-mobile {
        width: 3.5rem;
        padding: 0.8rem;
    }
    .logo-desktop {
        width: 12rem;
        padding: 2rem 2rem;
    }
}
</style>
