<template>
  <div class="about">
    <HeroImage />
    <h1>This is an about page</h1>
  </div>
</template>
<script>
import HeroImage from '@/components/HeroImage.vue';

export default {
  name: 'About',
  components: {
    HeroImage,
  },
};
</script>
<style lang="scss">
  .about {
    position: relative;
    display: flex;
    margin: 0;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    width: 100%;
    height: calc(100vh - 80px);
  }
</style>
