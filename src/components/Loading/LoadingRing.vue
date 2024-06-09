<template>
  <div class="loading-ring">
    <div class="loading-ring-item" v-for="item in 9" :style="getStyle(item)"></div>
  </div>
</template>

<script lang="tsx" setup>
const getStyle = (item) => {
  const d = 2 * item + 5
  return {
    margin: -(0.5 * d) + 'em',
    width: `${d}rem`,
    height: `${d}rem`,
    'animation-duration': `${6.3 / (10 - item)}s`,
  }
}
</script>

<style scoped lang="less">
.loading-ring {
  .loading-ring-item {
    position: absolute;
    top: 50%;
    left: 50%;
    border: solid 0;
    border-color: #8fd3f4 transparent;
    border-width: 0.2rem 0 0;
    border-radius: 50%;
    animation: rotateAnimation 0s linear infinite;
  }
}
</style>
