<template>
  <div class="nav">
    <router-link to="/" class="link">Home</router-link>|
    <router-link to="/about" class="link">About</router-link>
  </div>
</template>
<script>
export default {
  name: 'Nav',
};
</script>
<style lang="scss">
    .nav {
        background-color: black;
        height: 60px;
        color: white;
        display: flex;
        align-items: center;
        padding-left: 15px;
    }

    .link {
        padding-right: 20px;

        &:not(:first-of-type) {
            padding-left: 20px;
        }

        &:visited {
            color: white;
        }
    }
</style>
