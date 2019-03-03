<template>
  <div :style="style" class="item" />
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
        photo: this.item.links[0].href,
        title: this.item.data[0].title,
      };
    },
    computed: {
      style() {
        return `background-image: url("${this.photo}")`;
      },
    },
  };
</script>

<style lang="scss" scoped>
  .item {
    width: 15vw;
    height: 15vw;
    background-size: cover;
    background-repeat: no-repeat;
    background-position: 50%;

    @media (min-width: 768px) {
      width: 10vw;
      height: 10vw;
    }
  }
</style>
