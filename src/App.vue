<template>
  <div id="app">
    <HeroImage v-if="views.heroImage" />
    <Claim v-if="views.claim" @start-exploring="openGallery">
        <button slot="button" @click="openGallery(), getDogImages()" class="button">Start exploring</button>
    </Claim>
    <transition name="slide">
      <Gallery
      @next-image="getDogImages"
      @like="addToFavs"
      @show-imgs="showImages"
      :loading="state.loading"
      :img="links.image"
      :video="links.video"
      :likedDogs="links.likedDogs"
      :likedImg="state.likedImg"
      v-if="views.gallery"/>
    </transition>
    <div v-if="views.likedImages" class="likedImages">
      <h2>Images and videos you liked</h2>
      <div class="likedImages__sadBlock">
        <span v-if="links.likedDogs.length === 0" class="likedImages__sadText">You liked nothing</span>
        <i v-if="links.likedDogs.length === 0" class="far fa-sad-tear"></i>
      </div>

      <LikedImages v-for="item in links.likedDogs" :key="item" :item="item"/>
    </div>

  </div>
</template>

<script>
import HeroImage from './components/HeroImage.vue';
import Claim from './components/Claim.vue';
import Gallery from './components/Gallery.vue';
import LikedImages from './components/LikedImages.vue';
import debounce from 'lodash.debounce';


import axios from 'axios';


export default {
  name: 'app',
  data() {
    return {
        views: {
          heroImage: true,
          gallery: false,
          claim: true,
          likedImages: false,
        },

        links: {
          image: '',
          video: '',
          likedDogs: [],
        },

        state: {
          loading: true,
          likedImg: false,
        }
    }
  },

  components: {
    HeroImage,
    Claim,
    Gallery,
    LikedImages,
  },

  methods: {
    getDogImages: debounce(function() {
      this.state.loading = true;
      axios.get('https://random.dog/woof')
      .then(response => {
        if (response.data.slice(response.data.length-3) === 'mp4' || response.data.slice(response.data.length-4) === 'webm') {
          this.links.video = `https://random.dog/${response.data}`;
          this.links.image = '';
          this.state.loading = false;
          this.state.likedImg = false;
        } else {
          this.links.image = `https://random.dog/${response.data}`;
          this.links.video = '';
          this.state.loading = false;
          this.state.likedImg = false;

        }

      })
      .catch(error => {
        console.log(error);
      })
    }, 500),

    openGallery() {
      this.views.heroImage = false;
      this.views.gallery = true;
      this.views.claim = false;

    },

    addToFavs() {

      if (this.links.likedDogs.indexOf(this.links.image) === -1 && this.links.image !== '') {
          this.links.likedDogs.push(this.links.image);
      } else if (this.links.likedDogs.indexOf(this.links.video) === -1 && this.links.video !== '') {
          this.links.likedDogs.push(this.links.video);
      }
      console.log(this.links.likedDogs);
      return this.state.likedImg = true;
    },

    showImages(e) {
      this.views.gallery = e;
      this.views.heroImage = e;
      this.views.likedImages = true;
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


// HERO IMAGE BUTTON
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

  .likedImages {
    display: grid;
    grid-template-columns: 1fr;
    grid-gap: 20px;
    height: 100%;

    @media(min-width: 1024px) {
      width: 50%;
      background-color: #f6f6f6;
      margin: auto;
      justify-items: center;
      }

    h2 {
      margin-top: 40px;
      text-align: center;

      @media(min-width: 768px) {
        font-size: 50px;
      }

      @media(min-width: 1024px) {
        font-size: 70px;
      }
    }

    &__sadBlock {
      text-align: center;
    }

    &__sadText {
      display: block;
      text-align: center;
      font-size: 45px;
      color: #c4c4c4;
      text-transform: lowercase;

      @media(min-width: 768px) {
        font-size: 120px;
      }

      @media(min-width: 1024px) {
        font-size: 150px;
      }
    }

    .fa-sad-tear {
      text-align: center;
      font-size: 200px;
      color: #c4c4c4;

      @media(min-width: 768px) {
        font-size: 500px;
      }
    }
  }


  /// ANIMATION

  .slide-enter-active,
  .slide-leave-active {
    transition: opacity .3s ease;
  }

  .slide-enter,
  .slide-leave-to {
    opacity: 0;
  }
</style>
