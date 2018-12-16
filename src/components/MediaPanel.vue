<template>
    <div class="mediaPanel">
        <i @click="$emit('show-imgs', false)" class="fas fa-dog">
            <span class="mediaPanel__counter">{{likedDogs.length}}</span>
        </i>
        <i @click="$emit('like')" :style="[likedImg ? liked : notLiked]"  class="fas fa-heart"></i>
        <i @click="$emit('next-image')" class="fas fa-arrow-right"></i>
    </div>
</template>

<script>
export default {
    data() {
        return {
            liked: {
                color: 'red',
            },

            notLiked: {
                color: 'white',
            }
        }
    },

    props: {
        likedDogs: {
            type: Array,
            required: true,
        },

        likedImg: {
            type: Boolean,
            required: true,
        },
    },

    created() {
        console.log(this.likedImg);
    }

}
</script>

<style lang="scss" scoped>
    .mediaPanel {
                display: flex;
                justify-content: space-evenly;
                align-items: center;
                width: 100%;
                height: 60px;
                position: fixed;
                bottom: -1px;
                right: 0px;
                font-size: 40px;
                color: #fff;
                text-align: right;
                background-color: rgba(0, 0, 0, .8);
                z-index: 0;

                & :first-child {
                    position: relative;

                    &:hover {
                        cursor: pointer;
                    }

                    & span {
                        position: absolute;
                        right: -10px;
                        top: -8px;
                        font-size: 18px;
                        color: #fff;
                    }
                }

                & :nth-child(2) {

                    &:hover {
                        cursor: pointer;
                        color: red;
                    }
                }

                & :last-child {
                    cursor: pointer;

                    &:hover {
                        cursor: pointer;

                    }

                }

                &__counter {
                    position: absolute;
                    left: 10px;
                    font-size: 40px;
                }
            }
</style>
