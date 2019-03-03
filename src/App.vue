<template>
  <div id="app">
    <Background />
    <div class="nav">
      <router-link class="link" to="/">Spacer</router-link>
      <router-link class="link" to="/about">About</router-link>
    </div>
    <transition name="fade">
      <router-view />
    </transition>
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
    data() {
      return {
        step: 0,
      };
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

  .nav {
    margin: 10px;
    text-align: right;
    color: #000;
  }

  .nav .link {
    margin: 5px;
    color: #fff;
    text-decoration: none;
  }

  .nav .link:hover {
    box-shadow: 0 5px 5px -5px #fff;
  }
</style>
