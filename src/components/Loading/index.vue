<template>
  <!--  :class="state.imgLoaded ? 'loaded' : null" -->
  <div class="loading-wrapper" :class="state.imgLoaded ? 'loaded' : null" @click="handleAppearance">
    <!-- <LoadingLight /> -->
    <!-- <LoadingCircle /> -->
    <LoadingRing />
    <span class="loading-wrapper-tip"> Loading... </span>
  </div>
</template>

<script setup>
import { nextTick, watch, inject } from 'vue'
import LoadingCircle from './LoadingCircle.vue'
import LoadingRing from './LoadingRing.vue'
// import LoadingLight from './LoadingLight.vue'

const state = inject('state')

// 配置
watch(
  () => state.imgLoaded,
  (value) => {
    if (value) {
      setTimeout(() => {
        handleAppearance()
      }, 1000)
    }
  },
)

const handleAppearance = async () => {
  const clipPath = [`circle(0%)`, `circle(100%)`]
  await document.startViewTransition(async () => {
    await nextTick()
  }).ready

  document.documentElement.animate(
    { clipPath: clipPath },
    {
      duration: 1000 * 0.8,
      easing: 'ease-out',
      pseudoElement: '::view-transition-new(root)',
    },
  )
}
</script>

<style lang="less" scoped>
.loading-wrapper {
  position: fixed;
  top: 0;
  left: 0;
  display: flex;
  justify-content: center;
  align-items: center;
  width: 100%;
  height: 100%;
  z-index: 999;
  overflow: hidden;
  background: #526e99;
  .loading-wrapper-tip {
    font-weight: bold;
    font-size: 20px;
  }

  &.loaded {
    opacity: 0;
    background-color: transparent;
    transform: scale(0);
    transition: all 0.5s 1s ease-out, background-color 0.2s 1s ease-out;
  }
}

::view-transition-old(root),
::view-transition-new(root) {
  animation: none;
  mix-blend-mode: normal;
}
</style>
