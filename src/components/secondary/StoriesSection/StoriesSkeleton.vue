<template>
    <div>
        <div class="loader-container">
            <span class="loader"></span>
        </div>
        <div class="container">
            <div class="story-thumb" v-for="(story, index) in 5" :key="index">
                <div class="skeleton-image"></div>
                <div class="skeleton-text"></div>
            </div>
        </div>
    </div>
</template>
<script>
export default {
    name: "StoriesComponent",

    data() {
        return {};
    },
};
</script>

<style scoped lang="scss">
@import "../../../scss/resources";

.loader-container {
    padding: 1rem 0;
    display: flex;
    justify-content: center;
    align-items: center;
}

.container {
    width: 100%;
    background-color: white;

    display: flex;
    /* justify-content: center; */

    border-radius: 0.5rem;
    border: 0.05rem solid gray;

    padding: 0.7rem;

    .story-thumb {
        width: calc(100% / 5);
        display: flex;
        justify-content: center;
        align-items: center;
        flex-direction: column;
    }

    .skeleton-text {
        height: 0.5rem;
        width: 50%;
        margin: 0.5rem;

        background-color: $color-gray-light;

        animation: flash-bg 1s infinite;
    }

    @keyframes flash-bg {
        0% {
            background-color: #ddd;
        }
        50% {
            background-color: #d0d0d0;
        }
        100% {
            background-color: #ddd;
        }
    }
    .skeleton {
        background-color: $color-gray-light;
        margin: 2px;
    }
    .skeleton-image {
        background-color: $color-gray-light;
        width: 3.5rem;
        aspect-ratio: 4 / 4;
        border-radius: 50%;

        animation: flash-bg 0.5s infinite;
    }

    .skeleton-text {
        height: 0.5rem;

        background-color: $color-gray-light;

        animation: flash-bg 1s infinite;
    }

    .skeleton-post-image {
        background-color: $color-gray-light;
        height: 25rem;

        animation: flash-bg 0.5s infinite;
    }
}

.loader {
    width: 48px;
    height: 48px;

    border: 5px dotted rgb(163, 163, 163);
    border-radius: 50%;
    display: inline-block;
    position: relative;
    box-sizing: border-box;
    animation: rotation 2s linear infinite;
}

@keyframes rotation {
    0% {
        transform: rotate(0deg);
    }
    100% {
        transform: rotate(360deg);
    }
}
</style>
