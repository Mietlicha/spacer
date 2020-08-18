<template>
  <div class="app">
    <div class="wrapper">
      <HeroImage />
      <Claim />
      <SearchInput v-model="searchValue" @input="handleInput" />
    </div>
  </div>
</template>

<script>
import axios from 'axios';
import debounce from 'lodash.debounce';
import Claim from '@/components/Claim.vue';
import SearchInput from '@/components/SearchInput.vue';
import HeroImage from '@/components/HeroImage.vue';

const API = 'https://images-api.nasa.gov/search';

export default {
  name: 'App',
  components: {
    Claim,
    SearchInput,
    HeroImage,
  },
  data() {
    return {
      searchValue: '',
      results: [],
    };
  },
  methods: {
    handleInput: debounce(function () {
      console.log(this.searchValue);
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

<style lang="scss" >
@import url('https://fonts.googleapis.com/css2?family=Montserrat:wght@300;400;600;800&display=swap');

* {
  box-sizing: border-box;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}

body {
  font-family: 'Montserrat', sans-serif;
  margin: 0;
  padding: 0;
}

.wrapper {
  display: flex;
  justify-content: center;
  flex-direction: column;
  align-items: center;
  margin: 0;
  padding: 30px;
  width: 100%;
  height: 100vh;
}
</style>
