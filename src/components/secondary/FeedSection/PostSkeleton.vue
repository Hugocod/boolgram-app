<template>
    <div class="post-skeleton">
        <div class="post-header">
            <div class="skeleton-image"></div>

            <div class="text-block">
                <div class="skeleton-text"></div>
                <div class="skeleton-text"></div>
            </div>
        </div>

        <div class="skeleton-post-image"></div>
    </div>
</template>

<script>
export default {
    name: "PostSkeleton",
};
</script>

<style scoped lang="scss">
@import "../../../scss/resources";

.post-skeleton {
    margin: 4rem 0;
    background-color: white;

    border-radius: 0.5rem;
    border: 0.05rem solid gray;

    width: 29rem;

    @media (max-width: 470px) {
        width: 20rem;
    }

    @media (max-width: 340px) {
        width: 18rem;
    }

    .text-block {
        & > div:last-child {
            width: 50%;
        }
    }

    .post-header {
        display: flex;
        align-items: center;

        padding: 0.8rem;
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
