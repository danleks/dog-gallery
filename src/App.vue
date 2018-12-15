<template>
  <div id="app">
    <HeroImage />
    <Claim />
  </div>
</template>

<script>
import HeroImage from './components/HeroImage.vue';
import Claim from './components/Claim.vue';


export default {
  name: 'app',
  components: {
    HeroImage,
    Claim,
  },
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
</style>
