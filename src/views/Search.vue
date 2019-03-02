<template>
  <div class="wrapper">
    <Claim />
    <SearchInput />
    <ul>
      <li v-for="item in results" :key="item.data[0].nasa_id">
        <p>{{ item.data[0].description }}</p>
      </li>
    </ul>
  </div>
</template>

<script>
import axios from 'axios';
import debounce from 'lodash.debounce';
import Claim from '@/components/Claim';
import SearchInput from '@/components/SearchInput';

const API = 'https://images-api.nasa.gov/search';

  export default {
    name: 'Search',
    components: { Claim, SearchInput },
    data() {
      return {
          searchValue: '',
          results: [],
      };
    },
    methods: {
      handleInput: debounce(function() {
        axios.get(`${API}?q=${this.searchValue}&media_type=image`)
          .then((response) => {
            this.results = response.data.collection.items;
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
    height: 100vh;
    flex-direction: column;
    align-items: center;
    margin: 0;
    padding: 30px;
    justify-content: center;
  }
</style>
