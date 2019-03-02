<template>
  <div class="claimWrapper">
    <h1 class="claim">SPACER</h1>
    <p class="subclaim">Begin your jorney!</p>
    <p class="subclaim">Type anything space-related to start.</p>
  </div>
</template>

<script>
  export default {
    name: 'Claim',
  }
</script>

<style lang="scss" scoped>
  .claimWrapper {
    color: #000;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
  }

  .claim {
    font-size: 50px;
    margin: 0;
  }

  .subclaim {
    margin-top: 20px;
    font-size: 13px;
  }
</style>
