<template>
  <input
    name='search'
    id='search'
    :class='{ dark: dark }'
    :value='value'
    @input='handleChange'
  />
<!-- pierwsze dark to nazwa klasy a drugie to warunek do spełnienia;
 jeśli dark true to dorzucana jest klasa, można zapisac { darka } poniewaz mają te same nazwy -->
</template>
<script>
export default {
  name: 'SearchInput',
  props: {
    value: {
      type: String,
      required: true,
    },
    dark: {
      type: Boolean,
      default: false,
    },
  },
  methods: {
    handleChange(e) {
      this.$emit('input', e.target.value);
    },
  },
};
</script>
<style lang="scss">
  input {
    border: none;
    border-bottom: 2px solid white;
    height: 30px;
    text-align: center;
    background-color: transparent;
    color: white;
    font-size: 20px;
    transition: box-shadow .3s;
    margin-top: 100px;

    @media (min-width: 768px) {
      margin-top: 50px;
    }

    &:focus {
      outline: none;
      box-shadow: 0 5px 15px -6px white;
    }
  }

  .dark {
    color: blue;
    border-bottom-color: blue;
  }
</style>
