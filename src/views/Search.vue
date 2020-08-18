<template>
  <div class="wrapper">
    <Claim />
    <div class="search">
      <label for="search">Search</label>
      <input id="search" name="search" v-model="searchValue" @input="handleInput" />
    </div>
  </div>
</template>

<script>
import axios from 'axios';
import debounce from 'lodash.debounce';
import Claim from '@/components/Claim.vue';

const API = 'https://images-api.nasa.gov/search';

export default {
  name: 'Search',
  components: {
    Claim,
  },
  data() {
    return {
      searchValue: '',
      results: [],
    };
  },
  methods: {
    handleInput: debounce(function () {
      const fetchAPI = async () => {
        const data = await axios.get(
          `${API}?q=${this.searchValue}&media_type=image`,
        );
        this.results = data.data.collection.items;
      };
      fetchAPI().catch((err) => console.log(`upps! ${err}`));
    }, 500),
  },
};
</script>
<style lang="scss" scoped>
.wrapper {
  display: flex;
  flex-direction: column;
  align-items: center;
  margin: 0;
  padding: 30px;
  width: 100%;
}

.search {
  display: none;
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
