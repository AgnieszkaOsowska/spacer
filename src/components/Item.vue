<template>
  <!-- <div :style='style' class='item'> -->
  <!-- </div> -->
  <div class="item">
    <img :src="photo" :alt="title">
  </div>
</template>
<script>
export default {
  name: 'Item',
  props: {
    item: {
      type: Object,
      required: true,
    },
  },
  data() {
    return {
      photo: '',
      title: '',
    //   style: {
    //     backgroundImage: `url('${this.photo}')`,
    //   },
    };
  },
  //  computed: {
  //  style() {
  //    return `background-image: url("${this.photo}")`;
  //   },
  //  },
  mounted() {
    this.photo = this.item.links[0].href;
    this.title = this.item.data[0].title;
  },
};
</script>
<style lang="scss">
    .item {
        width: 80vw;
        height: 250px;

        @media (min-width: 768px) {
            width: 40vw;
        }

        @media (min-width: 1200px) {
            width: 25vw;
        }

        img {
            width: 100%;
            height: 100%;
            object-fit: cover;
        }
        // background-size: cover;
        // background-repeat: no-repeat;
        // background-position: 50%;
    }
</style>
