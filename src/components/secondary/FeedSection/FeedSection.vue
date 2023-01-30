<template>
    <div class="container-feed">
        <div v-if="profilesData.isDataLoaded">
            <stories-section :profilesData="profilesData"> </stories-section>
        </div>
        <stories-skeleton v-else></stories-skeleton>

        <div v-if="postData.isDataLoaded">
            <post-block
                v-for="(post, index) in postData.data"
                :key="index"
                :postData="post">
            </post-block>
        </div>

        <post-skeleton v-else></post-skeleton>
    </div>
</template>

<script>
import StoriesSection from "../StoriesSection/StoriesSection.vue";
import StoriesSkeleton from "../StoriesSection/StoriesSkeleton.vue";
import PostBlock from "./PostBlock.vue";
import PostSkeleton from "./PostSkeleton.vue";

export default {
    name: "FeedSection",
    components: { PostBlock, PostSkeleton, StoriesSection, StoriesSkeleton },
    props: { postData: Object, profilesData: Object },
};
</script>

<style lang="scss" scoped>
.container-feed {
}
</style>
