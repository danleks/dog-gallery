<template>
    <div class="galleryWrapper">
        <Claim />
        <div v-if="loading === true" class="lds-heart"><div></div></div>
        <transition name="slideLeft">
            <MainImage v-if="loading === false" @next-image="$emit('next-image')" :img="img" :video="video" />
        </transition>
        <MediaPanel @like="$emit('like')" :likedImg="likedImg" :likedDogs="likedDogs" @next-image="$emit('next-image')"/>
    </div>

</template>

<script>
import Claim from './Claim.vue';
import MainImage from './MainImage.vue';
import MediaPanel from './MediaPanel.vue';


export default {
    name: 'Gallery',
    components: {
        Claim,
        MainImage,
        MediaPanel,

    },

    props: {
        img: {
            type: String,
            required: true,
        },

        video: {
            type: String,
            required: true,
        },

        loading: {
            type: Boolean,
            required: true,
        },

        likedDogs: {
          type: Array,
          required: true,
        },

        likedImg: {
            type: Boolean,
            required: true,
        },
    }
}
</script>

<style lang="scss" scoped>
    .galleryWrapper {
      position: relative;
      height: 90vh;
      display: flex;
      flex-direction: column;
      align-items: center;
      background-color: rgba(#fff, .8);
      z-index: 2;

      }

    .slideLeft-leave-active {
      transition: all 1s ease;
    }

    .slideLeft-enter,
    .slideLeft-leave-to {
      transform: translateX(-400px);
      opacity: 0;
    }

  /// SPINNER
.lds-heart {
  display: inline-block;
  position: fixed;
  top: 40%;
  width: 64px;
  height: 64px;
  transform: rotate(45deg);
  transform-origin: 32px 32px;
}
.lds-heart div {
  top: 23px;
  left: 19px;
  position: absolute;
  width: 26px;
  height: 26px;
  background: red;
  animation: lds-heart 1.2s infinite cubic-bezier(0.215, 0.61, 0.355, 1);
}
.lds-heart div:after,
.lds-heart div:before {
  content: " ";
  position: absolute;
  display: block;
  width: 26px;
  height: 26px;
  background:red;
}
.lds-heart div:before {
  left: -17px;
  border-radius: 50% 0 0 50%;
}
.lds-heart div:after {
  top: -17px;
  border-radius: 50% 50% 0 0;
}
@keyframes lds-heart {
  0% {
    transform: scale(0.95);
  }
  5% {
    transform: scale(1.1);
  }
  39% {
    transform: scale(0.85);
  }
  45% {
    transform: scale(1);
  }
  60% {
    transform: scale(0.95);
  }
  100% {
    transform: scale(0.9);
  }
}

</style>
