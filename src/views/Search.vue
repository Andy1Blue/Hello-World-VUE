<template>
<div :class="[{ flexStart: step === 1 }, 'wrapper']">
  <Claim v-if="step === 0" />
  <div v-bind:class="[step === 1 ? 'searchContainer' : '']">
    <SearchInput v-model="searchValue" @input="handleInput" :light="step === 1" />
  </div>
  <div class="results" v-if="results && !loading && step === 1">
    <Item v-for="item in results" :item="item" :key="item.data[0].nasa_id" @click.native="handleModalOpen(item)" />
  </div>
  <div class="loader" v-if="step == 1 && loading" />
  <transition name="fade">
    <Modal v-if="modalOpen" :item="modalItem" @closeModal="modalOpen = false" />
  </transition>
</div>
</template>

<script>
import axios from 'axios';
import debounce from 'lodash.debounce';
import Claim from '@/components/Claim';
import SearchInput from '@/components/SearchInput';
import Item from '@/components/Item';
import Modal from '@/components/Modal';

const API = 'https://images-api.nasa.gov/search';

export default {
  name: 'Search',
  components: {
    Claim,
    SearchInput,
    Item,
    Modal,
  },
  data() {
    return {
      modalOpen: false,
      modalItem: null,
      loading: false,
      step: 0,
      searchValue: '',
      results: [],
    };
  },
  methods: {
    handleModalOpen(item) {
      this.modalOpen = true;
      this.modalItem = item;
    },
    handleInput: debounce(function() {
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
  },
};
</script>

<style lang="scss" scoped>
@import url('https://fonts.googleapis.com/css?family=Montserrat:300,400,600');

.fade-enter-active,
.fade-leave-active {
    transition: opacity 0.2s;
}
.fade-enter,
.fade-leave-to {
    opacity: 0;
}

.wrapper {
    display: flex;
    width: 100%;
    min-height: 88vh;
    flex-direction: column;
    align-items: center;
    margin: 0;
    padding: 30px;
    justify-content: center;

    &.flexStart {
        justify-content: flex-start;
    }
}

.results {
    margin-top: 135px;
    display: grid;
    grid-template-columns: 1fr 1fr 1fr 1fr;
    grid-gap: 20px;

    @media (min-width: 768px) {
        grid-template-columns: 1fr 1fr 1fr 1fr 1fr 1fr 1fr 1fr;
    }
}

.searchContainer {
    margin-top: 15px;
    width: 100%;
    height: 100px;
    background-color: #000;
    position: absolute;
    display: flex;
    flex-direction: column;
    align-items: center;
    padding: 5px;
    justify-content: center;
    opacity: 0.6;
}

.loader {
    margin-top: 135px;
    display: inline-block;
    position: relative;
    width: 64px;
    height: 64px;

    @media (min-width: 768px) {
        width: 90px;
        height: 90px;
    }
}

.loader:after {
    content: " ";
    display: block;
    border-radius: 50%;
    width: 0;
    height: 0;
    margin: 6px;
    box-sizing: border-box;
    border: 26px solid #1c1c1c;
    border-color: #1c1c1c transparent #1c1c1c transparent;
    animation: loader 1.2s infinite;
}

@keyframes loader {
    0% {
        transform: rotate(0);
        animation-timing-function: cubic-bezier(0.55, 0.055, 0.675, 0.19);
    }
    50% {
        transform: rotate(900deg);
        animation-timing-function: cubic-bezier(0.215, 0.61, 0.355, 1);
    }
    100% {
        transform: rotate(1800deg);
    }
}
</style>
