<template>
    <div class="outerWrapper">
        <div class="innerWrapper">
            <div class="photo">
                <img :src="photo" :alt="title">
            </div>
            <div class="description">
                <h2 class="title">{{title}}</h2>
                <p class="text">{{description}}</p>
            </div>
        </div>
        <div class="close" @click='$emit("closeModal")'></div>
    </div>
</template>
<script>
export default {
  name: 'Modal',
  props: {
    item: {
      type: Object,
      required: true,
    },
  },
  data() {
    return {
      photo: null,
      title: null,
      description: null,
    };
  },
  mounted() {
    this.photo = this.item.links[0].href;
    this.title = this.item.data[0].title;
    this.description = this.item.data[0].description;
  },
};
</script>
<style lang="scss">
  .outerWrapper {
      background-color: #f6f6f6;
      max-width: 100%;
      height: 100%;
      position: fixed;
      top: 0;
      left: 0;

      @media (min-width: 1200px) {
          max-width: 70%;
          max-height: 40%;
          top: 50%;
          left: 50%;
          transform: translate3d(-50%, -50%, 0);
          box-shadow: 0 30px 30px rgba(0, 0, 0, .3);
      }
  }

  .innerWrapper {
      display: flex;
      height: 100%;
      justify-content: center;
      align-items: center;
      padding: 50px;
      flex-direction: column;

      @media (min-width: 1200px) {
          flex-direction: row;
      }
  }

  .photo {
      width: 100%;
      height: auto;

      @media (min-width: 1200px) {
          min-width: 50%;
          padding-right: 30px;
          height: 100%;
      }

      img {
          width: 100%;
          max-height: 100%;
      }
  }

  .close {
      position: absolute;
      top: 0px;
      right: 0px;
      padding-top: 30px;
      cursor: pointer;

      &:before,
      &:after {
          content: '';
          display: block;
          width: 20px;
          height: 2px;
          background-color: black;
          position: absolute;
          right: 20px;
          top: 30px;
      }

      &:before {
          transform: rotate(45deg);
      }

      &:after {
          transform: rotate(-45deg);
      }
  }
</style>
