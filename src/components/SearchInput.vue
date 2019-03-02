<template>
  <div class="searchWrapper">
    <div class="search">
        <input id="search" name="search" v-model="searchValue" @input="handleInput" />
    </div>
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

const API = 'https://images-api.nasa.gov/search';

  export default {
    name: 'SearchInput',
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

  .searchWrapper {
    margin-top: 50px;
    display: flex;
    flex-direction: column;
    width: 250px;
    align-items: center;

    input {
      color: #000;
      text-align: center;
      font-size: 18px;
      font-weight: 300;
      height: 30px;
      border: 0;
      background: none;
      border-bottom: 1px solid #000;
      transition: box-shadow .3s ease-out;

      @media (min-width: 1024px) {
        font-weight: 400;
      }
    }

    input:focus {
      outline: none;
      box-shadow: 0 8px 10px -10px #000;
    }
  }
</style>
