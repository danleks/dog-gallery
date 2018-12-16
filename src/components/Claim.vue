<template>
    <div class="claim">
        <h1 class="claim__heading">
            Man's best friend
        </h1>

        <p class="claim__text">
            Swipe through the galary of dogs and choose your favourite ones.
        </p>
        <slot name="button"></slot>
    </div>
</template>

<script>
export default {
    name: 'Claim',
}
</script>

<style lang="scss" scoped>
    .claim {
        display: flex;
        flex-direction: column;
        align-items: center;

        &__heading {
            margin: 40px 0 8px 0;
            text-transform: uppercase;

            @media (min-width: 768px) {
                font-size: 60px;
            }
        }

        &__text {
            text-align: center;
            font-size: 10px;
            font-weight: bold;

             @media (min-width: 768px) {
                font-size: 18px;
            }
        }
    }
</style>
