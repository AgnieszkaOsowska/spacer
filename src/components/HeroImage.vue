<template>
    <div class="heroImage"></div>
</template>
<script>
export default {
  name: 'HeroImage',
};
</script>
<style lang="scss">
    .heroImage {
      background-image: url('../assets/cosmos.jpg');
      background-size: cover;
      position: absolute;
      top: 0px;
      left: 0;
      z-index: -10;
      width: 100%;
      height: 100%;

      &:after {
          content: '';
          display: block;
          position: absolute;
          top: 0px;
          left: 0;
          z-index: 1;
          width: 100%;
          height: 100%;
          background-color: black;
          opacity: 0.2;
      }
    }
</style>
