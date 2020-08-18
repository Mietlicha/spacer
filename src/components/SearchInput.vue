<template>
  <div class="searchWrapper">
    <label for="search">Search</label>
    <input id="search" name="search" v-model="searchValue" @input="handleInput" />
  </div>
</template>

<script>
export default {
  name: 'SearchInput',
};
</script>

<style lang="scss" scoped>
.searchWrapper {
  display: flex;
  flex-direction: column;
  width: 250px;
  margin-top: 50px;

  label {
    display: none;
  }

  input {
    margin-top: 50px;
    display: flex;
    width: 250px;
    color: white;
    text-align: center;
    font-size: 18px;
    font-weight: 300;
    height: 30px;
    border: 0;
    background: none;
    border-bottom: 1px solid white;
    transition: box-shadow 0.3s ease-out;
    @media (min-width: 1024px) {
      font-weight: 400;
    }
  }

  input:focus {
    outline: none;
    box-shadow: 0 10px 20px -8px rgba(255, 255, 255, 0.5);
  }
}
</style>