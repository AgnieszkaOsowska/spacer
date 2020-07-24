<template>
  <div :class='[{ flexStart: step === 1}, "wrapper"]'>
    <transition >
      <img src="@/assets/logo.png" alt="logo" class='logo' name='slide' v-if='step === 1'>
    </transition>
    <transition name='fade'>
      <HeroImage v-if='step === 0'/>
    </transition>
    <Claim v-if='step === 0'/>
    <SearchInput v-model='searchValue' @input='handleInput' :dark='step === 1'/>
    <div class='results' v-if='results && !loading && step === 1'>
      <Item
        v-for='item in results'
        :item='item'
        :key='item.data[0].nasa_id'
        @click.native='handleModalOpen(item)'
      />
    </div>
    <div class='loader' v-if='step === 1 && loading'></div>
    <Modal
      v-if='modalOpen'
      @closeModal='modalOpen = false'
      :item='modalItem'
    />
  </div>
</template>

<script>

import axios from 'axios';
import debounce from 'lodash.debounce';
import Claim from '@/components/Claim.vue';
import SearchInput from '@/components/SearchInput.vue';
import HeroImage from '@/components/HeroImage.vue';
import Item from '@/components/Item.vue';
import Modal from '@/components/Modal.vue';

const API = 'https://images-api.nasa.gov/search';

export default {
  name: 'Search',
  components: {
    Claim,
    SearchInput,
    HeroImage,
    Item,
    Modal,
  },
  data() {
    return {
      loading: false,
      step: 0,
      searchValue: '',
      results: [],
      modalOpen: false,
      modalItem: null,
    };
  },
  methods: {
    handleInput: debounce(function search() {
      this.loading = true;

      axios.get(`${API}?q=${this.searchValue}&media_type=image`)
        .then((response) => {
          this.results = response.data.collection.items;
          this.loading = false;
          this.step = 1;
        })
        .catch((error) => {
          console.log(error);
        });
    }, 500),
    handleModalOpen(item) {
      this.modalOpen = true;
      this.modalItem = item;
    },
  },
};
</script>

<style lang="scss">
  .wrapper {
    position: relative;
    display: flex;
    margin: 0;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    width: 100%;
    height: calc(100vh - 80px);

    &.flexStart {
      justify-content: flex-start;
    }
  }

  .fade-enter-active, .fade-leave-active {
    transition: opacity .5s ease;
    }

  .fade-enter, .fade-leave {
    opacity: 0;
  }

  .loader {
    display: inline-block;
    margin-top: 30px;
    width: 64px;
    height: 64px;

    @media (min-width: 768px) {
      width: 90px;
      height: 90px;
    }
  }

  .loader:after {
    content: '';
    display: block;
    width: 46px;
    height: 46px;
    margin: 1px;
    border-radius: 50%;
    border: 5px solid blue;
    border-color: blue transparent blue transparent;
    animation: loading 1.2s linear infinite;

    @media (min-width: 768px) {
      width: 90px;
      height: 90px;
    }
  }

  @keyframes loading {
    0% {
      transform: rotate(0deg);
    }
    100% {
      transform: rotate(360deg);
    }
  }

  .logo {
    position: absolute;
    right: 50%;
    top: 10px;
    transform: translateX(50%);
    max-height: 60px;

    @media (min-width: 768px) {
      max-height: 100px;
      right: 50px;
    }
  }

      .slide-enter-active, .slide-leave-active {
      transition: top .5s ease;
    }

    .slide-enter, .slide-leave {
      top: -200px;
    }

    .results {
      display: grid;
      grid-template-columns: 1fr;
      grid-gap: 20px;
      margin-top: 50px;

      @media (min-width: 768px) {
        grid-template-columns: 1fr 1fr;
      }

      @media (min-width: 1200px) {
        grid-template-columns: 1fr 1fr 1fr;
      }
    }
</style>
