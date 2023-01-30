<template>
    <div id="sp-container">
        <div class="picture-block">
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
    name: "SuggestedProfile",
    props: { picture: String, name: String },
};
</script>

<style scoped lang="scss">
@import "../../../scss/resources";

#sp-container {
    display: flex;
    justify-content: space-between;
    padding: 0.5rem 0;

    .picture-block {
        display: flex;
        align-items: center;
        width: 100%;
        gap: 1rem;
    }

    a {
        display: block;
        @include text-strong;
    }

    img {
        border-radius: 50%;
        width: 2.2rem;
        height: 2.2rem;
    }

    button {
        @include text-btn;
    }
}
</style>
