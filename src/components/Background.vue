<template>
  <div class="background" />
</template>

<script>
  export default {
    name: 'Background',
  }
</script>

<style lang="scss" scoped>
  .background {
    width: 100%;
    height: 100vh;
    position: fixed;
    top: 0;
    z-index: -1;
    background-image: url('../assets/bg.jpg');
    background-repeat: no-repeat;
    background-size: cover;
    background-position: 50% 0%;
  }
</style>
