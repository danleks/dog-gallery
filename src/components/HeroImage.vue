<template>
    <div class="heroImage">
    </div>
</template>

<script>
export default {
    name: 'HeroImage',
}
</script>

<style lang='scss' scoped>
    .heroImage {
        display: flex;
        justify-content: center;
        position: fixed;
        width: 100%;
        height: 100vh;
        background-image: url('../assets/heroImage.jpg');
        background-size: cover;
        background-position: 35%;
        z-index: -1;
    }
</style>
