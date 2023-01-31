<template>
    <div class="suggested-container">
        <div class="loggedUser-row">
            <div>
                <img
                    src="https://res.cloudinary.com/dflyrzhj9/image/upload/v1671628728/high-min_yynwgh.jpg" />
                <div>
                    <a href="https://www.hu-go.online/">Ugo Medioli</a>
                    <a href="https://www.hu-go.online/" target="_blank"
                        >www.hu-go.online</a
                    >
                </div>
            </div>

            <button>passa a</button>
        </div>

        <div class="showAll-section">
            <h4>Suggerimenti per te</h4>
            <a>Mostra Tutti</a>
        </div>

        <div v-if="profilesData.isDataLoaded">
            <profile-block
                v-for="(profile, index) in profilesData.data"
                :key="index"
                :name="profile.profile_name"
                :picture="profile.profile_picture"></profile-block>
        </div>
        <div v-else>
            <profile-skeleton
                v-for="(skeleton, index) in 8"
                :key="index"></profile-skeleton>
        </div>

        <p>developer by hugo with love</p>
    </div>
</template>

<script>
import ProfileBlock from "./ProfileBlock.vue";
import ProfileSkeleton from "./ProfileSkeleton.vue";
export default {
    components: { ProfileSkeleton, ProfileBlock },
    name: "SuggestedSection",
    props: { profilesData: Object },
};
</script>

<style lang="scss" scoped>
@import "../../../scss/resources";
.suggested-container {
    width: 400px;
    /* background-color: rgb(43, 255, 0); */
    padding: 3rem 2rem;

    @media (max-width: 1000px) {
        display: none;
    }

    button {
        @include text-btn;
    }

    a {
        @include text-strong;
    }

    .loggedUser-row {
        display: flex;
        justify-content: space-between;

        & div:first-child {
            display: flex;
            justify-content: center;
            align-items: center;
            gap: 1rem;

            a:last-child {
                @include text-medium;
            }
        }

        a {
            display: block;
            @include text-strong;
        }

        img {
            border-radius: 50%;
            width: 4rem;
        }
    }

    .showAll-section {
        display: flex;
        justify-content: space-between;
        align-items: center;

        padding: 1rem 0rem;
        @include text-medium;
        font-weight: 600;
    }
}
</style>
