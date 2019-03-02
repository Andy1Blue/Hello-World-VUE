<template>
  <div id="app">
    <Background />
    <div class="nav">
      <router-link to="/">Spacer</router-link>
      <router-link to="/about">About</router-link>
    </div>
    <router-view />
    <div class="bgAuthor">
       <a href="https://www.freepik.com/free-photos-vectors/abstract">Abstract photo created by kjpargeter - www.freepik.com</a>
    </div>
  </div>
</template>

<script>
import Background from '@/components/Background';

  export default {
    name: 'App',
    components: {
      Background,
    },
  }
</script>

<style lang="scss">
 @import url('https://fonts.googleapis.com/css?family=Montserrat:300,400,600,800');

  * {
    box-sizing: border-box;
  }

  body {
    font-family: 'Montserrat', sans-serif;
    margin: 0;
    padding: 0;
  }
</style>
