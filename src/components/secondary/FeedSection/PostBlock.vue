<template>
    <div class="post-container">
        <!-- header -->
        <div class="post-header">
            <div>
                <img
                    class="round-image"
                    :src="localPostData.profile_picture"
                    alt="" />
                <div>{{ postData.profile_name }}</div>
            </div>
            <font-awesome-icon icon="fa-solid fa-ellipsis" />
        </div>

        <!--  immagine del post -->
        <img :src="localPostData.post_image" />

        <div class="post-body">
            <!--  contenitore delle azioni -->
            <div class="actions-container">
                <div>
                    <font-awesome-icon icon="fa-regular fa-heart" />
                    <font-awesome-icon icon="fa-regular fa-comment" />
                    <font-awesome-icon icon="fa-regular fa-paper-plane" />
                </div>
                <div><font-awesome-icon icon="fa-regular fa-bookmark" /></div>
            </div>

            <!-- sezione dei like -->
            <div class="likes-description">
                Piace a
                <a href="">{{ localPostData.likes.length }}</a>
                persone
            </div>

            <!-- descrizione del post -->
            <p class="post-description">
                <span>{{ localPostData.profile_name }}</span>
                {{ localPostData.post_text }}
            </p>

            <!-- qui sotto i commenti -->
            <div class="post-comments">
                <!-- Gestisce i casi in cui : ci sono commenti, non ci sono nuovi commenti, i commenti sono assenti -->
                <div
                    v-if="localPostData.comments.length > 3"
                    @click="showAllComments">
                    Mostra tutti i commenti
                </div>
                <div v-else-if="localPostData.comments.length == 0">
                    Ancora nessun commento
                </div>
                <div v-else>Non ci sono altri commenti</div>

                <div v-for="(comment, index) in displayedComments" :key="index">
                    <div class="comment-container">
                        <p>
                            <a href="">{{ comment.username }}</a
                            >{{ comment.text }}
                        </p>
                    </div>
                </div>
            </div>

            <div class="post-date">
                <p>{{ calculateTimePost(localPostData.date.date) }}</p>
            </div>
        </div>
        <!-- sezione di input -->
        <div class="input-section">
            <div><font-awesome-icon icon="fa-regular fa-face-smile" /></div>

            <form @submit.prevent="addComment">
                <input
                    type="text"
                    v-model="newComment"
                    @input="onInput"
                    placeholder="Scrivi un messaggio..." />
                <button type="submit" :disabled="submitIsDisabled">
                    Pubblica
                </button>
            </form>
        </div>
    </div>
</template>

<script>
export default {
    name: "PostComponent",

    data() {
        return {
            localPostData: { ...this.postData },
            numberOfCommentsToShow: 3,
            newComment: "",
            submitIsDisabled: true,
        };
    },
    //
    props: {
        /* dati del post ricevuti via props (la chiamata API è nel parent); */
        postData: Object,
    },
    //
    computed: {
        displayedComments() {
            return this.localPostData.comments.slice(
                0,
                this.numberOfCommentsToShow
            );
        },
    },
    //
    methods: {
        showAllComments() {
            this.numberOfCommentsToShow = this.localPostData.comments.length;
        },
        addComment() {
            //
            if (this.newComment.trim() === "") {
                //
            } else {
                this.localPostData.comments.push({
                    username: "Anonymous",
                    text: this.newComment,
                });
                /* se l'utente inserisce un commento vengono mostrati tutti i commenti presenti */
                this.showAllComments();
                /* pulisce l'input */
                this.newComment = "";
                /* blocca il submit button di default */
                this.submitIsDisabled = true;
            }
        },
        onInput(e) {
            /*  Impedisce all'utente di mandare messaggi vuoti */
            //
            if (e.target.value.trim() === "") {
                this.submitIsDisabled = true;
            } else {
                this.submitIsDisabled = false;
            }
        },
        calculateTimePost(givenDate) {
            const currentDate = new Date();

            const diffInMs = currentDate - new Date(givenDate);

            const diffInHours = Math.round(diffInMs / 1000 / 60 / 60);
            const diffInMinutes = Math.round(diffInMs / 1000 / 60);
            const diffInDays = Math.round(diffInHours / 24);

            if (diffInHours < 1) {
                return `${Math.round(diffInMinutes)} minut${
                    diffInMinutes == 1 ? "o" : "i"
                } fa`;
            } else if (diffInHours >= 1 && diffInHours < 24) {
                return `${Math.round(diffInHours)} or${
                    diffInHours == 1 ? "a" : "e"
                } fa`;
            } else {
                return `${Math.round(diffInDays)} giorn${
                    diffInDays == 1 ? "o" : "i"
                } fa`;
            }
        },
    },
};
</script>

<style scoped lang="scss">
@import "../../../scss/resources";

.post-container {
    margin: 1.1rem 0;
    background-color: white;

    border-radius: 0.5rem;

    @include border-thin;

    width: 100%;
    @media (max-width: 470px) {
        width: 20rem;
    }

    @media (max-width: 340px) {
        width: 18rem;
    }

    font-size: 0.9rem;
    font-weight: 400;

    .post-header {
        display: flex;
        justify-content: space-between;
        align-items: center;

        @include text-strong;

        padding: 0.8rem;

        & > div:first-child {
            display: flex;
            justify-content: space-between;
            align-items: center;
            gap: 0.3rem;
        }
    }

    .post-body {
        padding: 0.8rem;
    }

    .post-description {
        padding-bottom: 0.6rem;
        span {
            @include text-strong;
        }
    }

    .likes-description {
        padding-bottom: 1rem;
        a {
            @include text-strong;
        }
    }

    .actions-container {
        display: flex;
        justify-content: space-between;
        align-items: top;

        & div:first-child * {
            padding: 0rem 0.8rem 1rem 0;
        }
    }

    .post-date {
        p {
            @include text-small-capitalized;
        }
    }

    .input-section {
        display: flex;
        justify-content: space-between;
        align-items: center;

        padding: 0.8rem;

        border-top: 1px solid rgb(215, 209, 209);

        form {
            width: 100%;

            display: flex;
            justify-content: space-between;
            align-items: center;

            input {
                border: none;
                /*  background-color: #f2f2f2; */
                padding: 0.2rem 0rem;
                font-size: 0.9rem;
                width: 100%;

                &:focus {
                    outline: none;
                    box-shadow: none;
                }
            }
        }
    }

    button {
        @include text-btn;
    }

    img {
        width: 100%;
    }

    .round-image {
        border-radius: 50%;

        width: 2.5rem;
        aspect-ratio: 4 / 4;
    }

    .post-comments {
        & > div:first-child {
            padding-bottom: 0.5rem;
            @include text-medium;
            cursor: pointer;
        }

        .comment-container {
            display: block;
            padding: 0.2rem 0;
            a {
                @include text-strong;
                padding-right: 0.4rem;
            }

            p {
                color: $color-black;
                word-break: break-all;
            }
        }
    }

    .fa-ellipsis,
    .fa-heart,
    .fa-comment,
    .fa-paper-plane,
    .fa-bookmark,
    .fa-face-smile {
        font-size: 1.4rem;
    }

    .fa-face-smile {
        margin-right: 0.8rem;
    }

    .fa-ellipsis {
        font-size: 1.1rem;
    }

    *:disabled {
        opacity: 0.4;
    }
}
</style>
