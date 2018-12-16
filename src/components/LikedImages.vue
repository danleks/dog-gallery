<template>
    <div class="imgWrapper">
        <img v-if="img" :src="img" alt="random photo">
        <video v-if="video" autoplay loop>
            <source :src="video" type="video/mp4">
            <source :src="video" type="video/webm">
            YOur browser does not support the video tag.
    </video>
    </div>
</template>

<script>
export default {
    name: 'LikedImages',
    data() {
        return {
            video: '',
            img: '',
            sadIcon: true,
        }
    },

    props: {
        item: {
            type: String,
            required: true,
        }
    },

    created() {
         if (this.item.substring(this.item.length - 3) === 'mp4' || this.item.substring(this.item.length - 4) === 'webm') {
                this.video = this.item;
                //this.sadIcon = false;
            } else {
                this.img = this.item;
                //this.sadIcon = false;

            }
    }
}
</script>

<style lang="scss" scoped>

    .imgWrapper {
        width: 100%;
        text-align: center;


        img {
            width: 100%;
        }

        video {
            width: 100%;
        }
    }

</style>
