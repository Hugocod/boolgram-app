<template>
    <home-page></home-page>
</template>

<script>
import HomePage from "./components/primary/HomePage.vue";

export default {
    name: "App",
    components: {
        HomePage,
    },
};
</script>

<style lang="scss">
#app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    color: #2c3e50;
}

body {
    box-sizing: border-box;
    padding: 0 !important;
    margin: 0 !important;
}
</style>
