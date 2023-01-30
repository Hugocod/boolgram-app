<template>
    <a class="container">
        <div class="icon-container">
            <slot name="icon">icon</slot>
        </div>
        <div class="text-container">
            <slot name="text">text</slot>
        </div>
    </a>
</template>

<script>
export default {
    name: "NavLink",
};
</script>

<style scoped lang="scss">
.container {
    display: flex;
    align-items: center;
    justify-content: start;

    padding: 0.5rem 4.5rem 0.5rem 0.5rem;
    margin: 1rem;

    border-radius: 2rem;

    transition: all ease-in-out 0.2s;

    @media (max-width: 1264px) {
        padding: 0.5rem 0;
    }

    &:hover {
        background-color: rgb(232, 230, 230);
    }

    .icon-container {
        /* background-color: rgb(153, 153, 180); */
        width: 2rem;
        height: 2rem;

        display: flex;
        justify-content: center;
        align-items: center;

        &:first-child {
            font-size: 1.5rem;
            color: black;
        }
        @media (max-width: 1264px) {
            display: flex;
            justify-content: center;
            align-items: center;

            width: 100%;
        }
    }
    .text-container {
        padding: 0 1rem;
        text-transform: capitalize;
        font-weight: 600;
        color: black;

        @media (max-width: 1264px) {
            display: none;
        }
    }
}
</style>
