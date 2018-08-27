<template>
  <div class="searchWrapper">
    <div  class="search">
      <input
        id="search"
        name="search"
        v-model="searchValue"
        @input="handleInput"
      />
    </div>
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
    }
  },
  methods: {
    handleInput: debounce(function() {  // całą metodę zamykamy w funkcji debounce
      axios.get(`${API}?q=${this.searchValue}&media_type=image`)
        .then((response) => {
          // console.log(response.data.collection.items)
          this.results = response.data.collection.items;
        })
        .catch(err => {

          console.log(err)
        })
    }, 1000)
  }
  }
</script>

<style lang="scss" scoped>
.searchWrapper {
    margin-top: 50px;
    display: flex;
    flex-direction: column;
    width: 250px;

    input {
      width: 100%;
      height: 30px;
      border: 0;
      border-bottom: 1px solid black;
      outline: none;
      background: none;
    }
  }
</style>