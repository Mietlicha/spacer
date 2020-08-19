<template>
  <div class="app">
    <div :class="[{flexStart: step === 1},'wrapper']">
      <transition name="slide">
        <img src="./assets/logo.svg" class="logo" v-if="step===1" />
      </transition>
      <transition name="fade">
        <HeroImage v-if="step===0" />
      </transition>
      <Claim v-if="step===0" />
      <SearchInput v-model="searchValue" @input="handleInput" :dark="step===1" />
      <div class="results" v-if="results && !loading && step===1">
        <Item
          v-for="item in results"
          :item="item"
          :key="item.data[0].nasa_id"
          @click.native="handleModalOpen(item)"
        />
      </div>
      <div v-if="step === 1 && loading" class="loader" />
      <Modal v-if="modalOpen" :item="modalItem" @closeModal="modalOpen = false" />
    </div>
  </div>
</template>

<script>
import axios from 'axios';
import debounce from 'lodash.debounce';
import Claim from '@/components/Claim.vue';
import SearchInput from '@/components/SearchInput.vue';
import HeroImage from '@/components/HeroImage.vue';
import Item from '@/components/Item.vue';
import Modal from '@/components/Modal.vue';

const API = 'https://images-api.nasa.gov/search';

export default {
  name: 'App',
  components: {
    Claim,
    SearchInput,
    HeroImage,
    Item,
    Modal,
  },
  data() {
    return {
      loading: false,
      step: 0,
      searchValue: '',
      results: [],
      modalOpen: false,
      modalItem: null,
    };
  },
  methods: {
    handleModalOpen(item) {
      this.modalOpen = true;
      this.modalItem = item;
    },
    handleInput: debounce(function () {
      this.loading = true;

      const fetchAPI = async () => {
        const data = await axios.get(
          `${API}?q=${this.searchValue}&media_type=image`,
        );
        this.results = data.data.collection.items;
        this.loading = false;
        this.step = 1;
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
  position: relative;

  &.flexStart {
    justify-content: flex-start;
  }
}

.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.5s;
}
.fade-enter, .fade-leave-to /* .fade-leave-active below version 2.1.8 */ {
  opacity: 0;
}

.slide-enter-active,
.slide-leave-active {
  transition: margin-top 0.3s ease;
}
.slide-enter, .slide-leave-to /* .fade-leave-active below version 2.1.8 */ {
  margin-top: -50px;
}

.logo {
  position: absolute;
  top: 30px;
}

.results {
  margin-top: 50px;
  display: grid;
  grid-template-columns: 1fr 1fr;
  grid-gap: 20px;

  @media (min-width: 768px) {
    width: 90%;
    grid-template-columns: 1fr 1fr 1fr;
  }
}

.loader {
  margin-top: 100px;
  display: inline-block;
  width: 64px;
  height: 64px;
  @media (min-width: 768px) {
    width: 90px;
    height: 90px;
  }
}
.loader:after {
  content: ' ';
  display: block;
  width: 46px;
  height: 46px;
  margin: 1px;
  border-radius: 50%;
  border: 5px solid #1e3d4a;
  border-color: #1e3d4a transparent #1e3d4a transparent;
  animation: loading 1.2s linear infinite;
  @media (min-width: 768px) {
    width: 90px;
    height: 90px;
  }
}
@keyframes loading {
  0% {
    transform: rotate(0deg);
  }
  100% {
    transform: rotate(360deg);
  }
}
</style>
