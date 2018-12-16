<template>
    <div class="media">
    <img v-if="img" :src="img" alt="random photo">
    <video v-if="video" autoplay loop>
        <source :src="video" type="video/mp4">
        <source :src="video" type="video/webm">
        YOur browser does not support the video tag.
    </video>
</div>
</template>

<script>
import MediaPanel from './MediaPanel.vue';
export default {
    name: 'MainImage',
    data() {
        return {

        }
    },
    components: {
    },
    props: {
        img: {
            type: String,
            required: true,
        },

        video: {
            type: String,
            required: true,
        }
    }
}
</script>

<style lang="scss" scoped>
    .media {
            position: relative;
            width: 100%;
            height: 70%;
            margin-top: 12px;

            @media(min-width: 1024px) {
                width: 500px;
            }

        }

        img {
            display: block;
            width: 100%;
            max-height: 98%;

            @media(min-width: 1024px) {
                max-width: 100%;
                height: auto;
            }
        }

        video {
            width: 100%;
            max-height: 98%;
        }


        .fade-enter-active,
.fade-leave-active {
  transition: opacity 1s ease;
}
.fade-enter,
.fade-leave-to {
  opacity: 0;
}





</style>
