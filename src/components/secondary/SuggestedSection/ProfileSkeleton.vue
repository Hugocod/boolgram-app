<template>
    <div class="spk-container">
        <div>
            <div class="skeleton-image">
                <span class="loader"></span>
            </div>

            <div class="text-block">
                <div class="skeleton-text"></div>
                <div class="skeleton-text"></div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: "ProfileSkeleton",
    props: { picture: String, name: String },
};
</script>

<style scopes lang="scss">
@import "../../../scss/resources";

.spk-container {
    & > div:first-child {
        display: flex;
        align-items: center;
    }

    .text-block {
        & > div:last-child {
            width: 50%;
        }
    }

    padding: 0.3rem 0;

    .skeleton {
        background-color: $color-gray-light;
        margin: 2px;
    }
    .skeleton-image {
        background-color: $color-gray-light;
        width: 2.6rem;
        aspect-ratio: 4 / 4;
        border-radius: 50%;

        animation: flash-bg 0.5s infinite;
    }

    .skeleton-text {
        width: 100px;
        height: 0.5rem;
        margin: 4px;
        background-color: $color-gray-light;

        animation: flash-bg 0.5s infinite;
    }

    .skeleton-post-image {
        background-color: $color-gray-light;
        height: 25rem;

        animation: flash-bg 0.5s infinite;
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
}
</style>
