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
    background-position: 50% 50%;
  }

  .background::after {
    content: '';
    background: black;
    position: absolute;
    opacity: 0.1;
    top: 0;
    left: 0;
    z-index: 1;
    width: 100%;
    height: 100vh;
  }
</style>
