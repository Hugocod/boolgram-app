<template>
    <div class="suggested-container">
        <div class="loggedUser-row">
            <div>
                <img
                    src="https://newprofilepic2.photo-cdn.net//assets/images/article/profile.jpg" />
                <div>
                    <a href="">Hugo_d_ev</a>
                    <a href="">Ugo Medioli</a>
                </div>
            </div>

            <button>passa a</button>
        </div>

        <div class="showAll-section">
            <h4>suggerimenti per te</h4>
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
.suggested-container {
    @import "../../../scss/resources";
    width: 400px;
    /* background-color: rgb(43, 255, 0); */
    padding: 3rem 2rem;

    @media (max-width: 1000px) {
        display: none;
    }

    button {
        background-color: rgba(255, 255, 255, 0);
        border: none;
        color: #000;
        font-size: 0.8rem;
        font-weight: 600;

        color: #34a0f7;
        text-transform: capitalize;
    }

    a {
        text-decoration: none;
        display: block;
        font-weight: 600;
        font-size: 0.9rem;
        color: black;
    }

    span {
        font-size: 0.8rem;
        font-weight: 500;
        color: rgb(144, 141, 141);
    }

    .loggedUser-row {
        display: flex;
        justify-content: space-between;

        & div:first-child {
            display: flex;
            justify-content: center;
            align-items: center;
            gap: 1rem;
        }

        a {
            display: block;
            font-weight: 600;
            font-size: 0.9rem;
            color: black;
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
    }
}
</style>
