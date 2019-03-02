<template>
  <div :class="[{ flexStart: step === 1 }, 'wrapper']">
    <div class="logo" v-if="step === 1">SPACER</div>
    <Claim v-if="step === 0" />
    <div v-bind:class="[step === 1 ? 'searchContainer' : '']">
      <SearchInput v-model="searchValue" @input="handleInput" :light="step === 1" />
    </div>
      <div class="results" v-if="results && !loading && step === 1">
        <Item v-for="item in results" :item="item" :key="item.data[0].nasa_id" />
      </div>
  </div>
</template>

<script>
import axios from 'axios';
import debounce from 'lodash.debounce';
import Claim from '@/components/Claim';
import SearchInput from '@/components/SearchInput';
import Item from '@/components/Item';

const API = 'https://images-api.nasa.gov/search';

  export default {
    name: 'Search',
    components: { Claim, SearchInput, Item },
    data() {
      return {
        loading: false,
        step: 0,
        searchValue: '',
        results: [],
      };
    },
    methods: {
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

.wrapper {
  display: flex;
  width: 100%;
  min-height: 100vh;
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
    display: grid;
    grid-template-columns: 1fr 1fr;
    grid-gap: 20px;

    @media (min-width: 768px) {
      grid-template-columns: 1fr 1fr 1fr;
    }
  }

  .searchContainer {
    width: 100%;
    background-color: #000;
    position: relative;
    margin: 0 0 20px 0;
    display: flex;
    flex-direction: column;
    align-items: center;
    padding: 5px;
    justify-content: center;
    opacity: 0.5;
  }

  .logo {
    font-size: 50px;
    margin: 10px 0 10px 0;
    font-weight: 600;
  }
</style>
