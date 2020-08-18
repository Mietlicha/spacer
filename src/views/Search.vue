<template>
  <div class="wrapper">
    <Claim />
    <SearchInput />
  </div>
</template>

<script>
import axios from 'axios';
import debounce from 'lodash.debounce';
import Claim from '@/components/Claim.vue';
import SearchInput from '@/components/SearchInput.vue';

const API = 'https://images-api.nasa.gov/search';

export default {
  name: 'Search',
  components: {
    Claim,
    SearchInput,
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
  justify-content: center;
  flex-direction: column;
  align-items: center;
  margin: 0;
  padding: 30px;
  width: 100%;
  background: url('../assets/heroimage.jpg') 80% 0% / cover no-repeat;
  height: 100vh;
}
</style>
