<template>
  <div class="wrapper">
    <div class="search">
      <label for="search">Search</label>
        <input id="search" name="search" v-model="searchValue" @input="handleInput" />
    </div>
  </div>
</template>

<script>
import axios from 'axios';

const API = 'https://images-api.nasa.gov/search';

  export default {
    name: 'Search',
    data() {
      return {
          searchValue: '',
      };
    },
    methods: {
      handleInput(e) {
        axios.get(`${API}?q=${this.searchValue}&media_type=image`)
          .then((response) => {
            console.log(response);
          })
          .catch((error) => {
            console.log(error);
          });
      },
    },
  };
</script>

<style lang="scss" scoped>
  .wrapper {
    display: flex;
    width: 100%;
    flex-direction: column;
    align-items: center;
    margin: 0;
    padding: 30px;
  }

  .search {
    display: flex;
    flex-direction: column;
    width: 250px;

    label {
      font-family: Montserrat, sans-serif;
    }

    input {
      height: 30px;
      border: 0;
      border-bottom: 1px solid black;
    }
  }
</style>