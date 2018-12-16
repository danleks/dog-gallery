<template>
  <div id="app">
    <HeroImage v-if="heroImage" />
    <Claim v-if="claim" @start-exploring="openGallery">
        <button slot="button" @click="openGallery(), getDogImages()" class="button">Start exploring</button>
    </Claim>
    <transition name="slide">
      <Gallery
      @next-image="getDogImages"
      @like="addToFavs"
      :loading="loading"
      :img="image"
      :video="video"
      :likedDogs="likedDogs"
      :likedImg="likedImg"
      v-if="galleryOpened"/>
    </transition>
  </div>
</template>

<script>
import HeroImage from './components/HeroImage.vue';
import Claim from './components/Claim.vue';
import Gallery from './components/Gallery.vue';
import debounce from 'lodash.debounce';


import axios from 'axios';


export default {
  name: 'app',
  data() {
    return {
      heroImage: true,
      galleryOpened: false,
      claim: true,
      image: '',
      video: '',
      loading: true,
      likedDogs: [],
      likedImg: false,

    }
  },

  components: {
    HeroImage,
    Claim,
    Gallery
  },

  methods: {
    getDogImages: debounce(function() {
      this.loading = true;
      axios.get('https://random.dog/woof')
      .then(response => {
        if (response.data.slice(response.data.length-3) === 'mp4' || response.data.slice(response.data.length-4) === 'webm') {
          this.video = `https://random.dog/${response.data}`;
          this.image = '';
          this.loading = false;
          this.likedImg = false;
        } else {
          this.image = `https://random.dog/${response.data}`;
          this.video = '';
          this.loading = false;
          this.likedImg = false;

        }

      })
      .catch(error => {
        console.log(error);
      })
    }, 1500),

    openGallery() {
      this.heroImage = false;
      this.galleryOpened = true;
      this.claim = false;

    },

    addToFavs() {

      if (this.likedDogs.indexOf(this.image) === -1 && this.image !== '') {
          this.likedDogs.push(this.image);
      } else if (this.likedDogs.indexOf(this.video) === -1 && this.video !== '') {
          this.likedDogs.push(this.video);
      }

      return this.likedImg = true;
    }
  }
};
</script>

<style lang="scss">
@import url('https://fonts.googleapis.com/css?family=Lato');
  html {
  box-sizing: border-box;
  }
  *, *:before, *:after {
    box-sizing: inherit;
    padding: 0;
    margin: 0;
  }

  body {
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    font-family: 'Lato', sans-serif;
  }

  .button {
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

  .slide-enter-active,
  .slide-leave-active {
    transition: opacity .3s ease;
  }

  .slide-enter,
  .slide-leave-to {
    opacity: 0;
  }
</style>
