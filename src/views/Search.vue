<template>
  <div class="wrapper">

    <div  class="search">
      <label for="search">Search</label>
      <input
        id="search"
        name="search"
        v-model="searchValue"
        @input="handleInput"
      />
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
  name: 'Search',
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
//Fonts
@import url('https://fonts.googleapis.com/css?family=Montserrat');

  .wrapper {
    display: flex;
    flex-direction: column;
    align-items: center;
    margin: 0;
    padding: 30px;
    width: 100%;
  }

  .search {
    display: flex;
    flex-direction: column;
    width: 300px;

    input {
      height: 30px;
      border: 0;
      border-bottom: 1px solid black;
      outline: none;
    }

    label {
      font-family: 'Montserrat', sans-serif;
    }
  }


</style>
