<template>
    <div class="claim">
        <h1 class="claim__heading">
            Man's best friend
        </h1>

        <p class="claim__text">
            Swipe through the galary of dogs and choose your favourite ones.
        </p>

        <button class="claim__button">Start exploring</button>
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

        &__button {
            padding: 10px 25px;
            border: none;
            margin-top: 50px;
            background-color: #000;
            color: #fff;
            text-transform: uppercase;
            box-shadow: 0 5px 20px rgba(0, 0, 0, .2);
            transition: all .1s;

            @media (min-width: 768px) {
                padding: 25px 50px;
                margin-top: 60px;
                font-size: 25px;
            }

            @media (max-height: 674px) {
                margin-top: 40px;

            }


            &:focus {
                outline: none;
                border: none;
                transform: translateY(-1px);
                box-shadow: 0 8px 25px rgba(0, 0, 0, .2);


            }
        }
    }
</style>
