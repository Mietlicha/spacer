<template>
  <div>
    <label for="search">Search</label>
    <input id="search" name="search" :value="value" @input="handleChange" :class="{dark}" />
  </div>
</template>

<script>
export default {
  name: 'SearchInput',
  props: {
    value: {
      type: String,
      required: true,
    },
    dark: {
      type: Boolean,
      default: false,
    },
  },
  methods: {
    handleChange(e) {
      this.$emit('input', e.target.value);
    },
  },
};
</script>

<style lang="scss" scoped>
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

.dark {
  color: #1e3d4a;
  border-bottom-color: #1e3d4a;

  &:focus {
    box-shadow: 0 10px 20px -8px rgba(#1e3d4a, 0.2);
  }
}
</style>