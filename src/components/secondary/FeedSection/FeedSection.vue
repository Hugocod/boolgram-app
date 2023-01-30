<template>
    <div class="container-feed">
        <post-block
            v-for="(post, index) in postData"
            :key="index"
            :postData="post"></post-block>
    </div>
</template>

<script>
import PostBlock from "./PostBlock.vue";

export default {
    name: "FeedSection",
    components: { PostBlock },
    props: { postData: Object },
};
</script>

<style lang="scss" scoped>
.container-feed {
    background-color: red;
    height: 900px;
    width: 1900px;

    border: 2px solid black;
}
</style>
