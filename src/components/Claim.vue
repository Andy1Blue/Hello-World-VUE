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
    text-align: center;
}

.claim {
    font-size: 50px;
    margin: 0;

    @media (min-width: 768px) {
        font-size: 80px;
    }

    @media (min-width: 1024px) {
        font-size: 100px;
    }
}

.subclaim {
    margin-top: 20px;
    font-size: 13px;
    font-weight: 400;

    @media (min-width: 768px) {
        width: 500px;
        font-size: 17px;
        letter-spacing: 1px;
        line-height: 1;
    }
}
</style>
