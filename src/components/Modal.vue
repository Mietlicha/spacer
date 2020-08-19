<template>
  <div class="outerWrapper">
    <div class="innerWrapper">
      <div class="photo"></div>
      <div class="description">
        <h2 class="title">title</h2>
        <p class="description">bla bla</p>
      </div>
    </div>
    <div class="close" />
  </div>
</template>
<script>
export default {
  name: 'Modal',
};
</script>
<style lang="scss" scoped>
.outerWrapper {
  background: #f6f6f6;
  max-width: 100%;
  height: 100%;
  position: fixed;
  top: 0;
  left: 0;
  @media (min-width: 1024px) {
    max-width: 70%;
    height: 60%;
    left: 0;
    right: 0;
    top: 0;
    bottom: 0;
    margin: auto;
    box-shadow: 0 30px 30px -10px rgba(0, 0, 0, 0.3);
  }
}

.innerWrapper {
  display: flex;
  height: 100%;
  padding: 50px;
  justify-content: center;
  align-items: center;
  flex-direction: column;
}
</style>