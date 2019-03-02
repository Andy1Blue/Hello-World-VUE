<template>
  <div class="searchWrapper">
    <div class="search">
        <input
        id="search"
        name="search"
        :value="value"
        :class="{ light: light }"
        @input="handleChange" />
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
    props: {
      value: {
        type: String,
        required: true,
      },
      light: {
        type: Boolean,
        default: false,
      },
    },
    data() {
      return {
        loading: false,
        step: 0,
        searchValue: '',
        results: [],
      }
    },
    methods: {
      handleChange(e) {
        this.$emit('input', e.target.value);
      },
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

    input.light {
      color: #fff;
      border-bottom-color: #fff;
    }

    input.light:focus {
      box-shadow: 0 8px 10px -10px #fff;
    }
  }
</style>
