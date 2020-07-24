<template>
  <div>
      <Nav />
      <router-view />
  </div>
</template>
<script>
import Nav from '@/components/Nav.vue';

export default {
  name: 'App',
  components: {
    Nav,
  },
};
</script>
<style lang="scss">
  @import url('https://fonts.googleapis.com/css2?family=Montserrat:wght@200;400;600;800&display=swap');

  * {
    box-sizing: border-box;
  }

  body {
    font-family: Montserrat, sans-serif;
  }
</style>
