<template>
<div id="app">
  <Background />
  <div class="nav">
    <div class="logo">
      <router-link class="link" to="/">SPACER</router-link>
    </div>
    <router-link class="link link-left" to="/">Home</router-link>
    <router-link class="link link-right" to="/about">About</router-link>
  </div>
  <transition name="fade">
    <router-view />
  </transition>
  <div class="bgAuthor">
    <p>Created by Krzysztof Bujak</p>
    <p><a href="https://www.freepik.com/free-photos-vectors/abstract" target="_blank">Abstract photo created by kjpargeter - www.freepik.com</a></p>
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
    position: relative;
    color: #000;

    .link-right {
        position: absolute;
        margin: 5px;
        color: #fff;
        text-decoration: none;
        text-align: right;
        right: 0;
    }

    .link-left {
        position: absolute;
        margin: 5px;
        color: #fff;
        text-decoration: none;
        text-align: left;
        left: 0;
    }

    .link:hover {
        box-shadow: 0 5px 5px -5px #fff;
    }
}
.logo {
    position: absolute;
    left: 50%;
    transform: translate(-50%, 0);
    font-family: 'Montserrat', sans-serif;
    font-size: 30px;
    font-weight: 800;

    @media (min-width: 768px) {
        font-size: 30px;
    }

    @media (min-width: 1024px) {
        font-size: 30px;
    }

    a:active,
    a:hover,
    a:link,
    a:visited {
        color: #000;
        text-decoration: none;
    }
}

.bgAuthor {
    text-align: center;
    color: #000;
    font-size: 12px;

    a:active,
    a:hover,
    a:link,
    a:visited {
        color: #000;
        text-decoration: none;
        font-size: 12px;
    }
}
</style>
