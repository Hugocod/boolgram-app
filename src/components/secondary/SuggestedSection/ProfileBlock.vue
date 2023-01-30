<template>
    <div class="sp-container">
        <div>
            <img :src="picture" />
            <div>
                <a href="">{{ name }}</a>
                <span>Ti segue</span>
            </div>
        </div>

        <button>segui</button>
    </div>
</template>

<script>
export default {
    name: "ProfileBlock",
    props: { picture: String, name: String },
};
</script>

<style scoped lang="scss">
@import "../../../scss/resources";

.sp-container {
    display: flex;
    justify-content: space-between;
    padding: 0.5rem 0;

    & div:first-child {
        display: flex;
        justify-content: center;
        align-items: center;
        gap: 1rem;
    }

    a {
        display: block;
        @include text-strong;
    }

    img {
        border-radius: 50%;
        aspect-ratio: 4/4;
        width: 2.2rem;
    }

    button {
        @include text-btn;
    }
}
</style>
