<template>
  <div class="background-wrapper">
    <!-- <ImageBackground v-bind="$attrs" /> -->
    <FilterBackground />
  </div>
</template>

<script setup>
// import ImageBackground from './ImageBackground.vue'
import FilterBackground from './FilterBackground.vue'
</script>

<style lang="less" scoped>
.background-wrapper {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  transition: 0.25s;
  z-index: 1;
}
</style>
