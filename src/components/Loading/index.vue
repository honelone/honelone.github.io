<template>
  <!--  :class="store.imgLoadStatus ? 'loaded' : null" -->
  <div
    id="loading-wrapper"
    :class="store.imgLoadStatus ? 'loaded' : null"
    @click="handleAppearance"
  >
    <!-- <LoadingLight /> -->
    <LoadingCircle />
    <span class="tip"> Loading... </span>
  </div>
</template>

<script setup>
import { nextTick, watch } from 'vue'
import { mainStore } from '@/stores'
import LoadingCircle from './LoadingCircle.vue'
import LoadingLight from './LoadingLight.vue'

const store = mainStore()

// 配置
watch(
  () => store.imgLoadStatus,
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
#loading-wrapper {
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
  background: #537895;
  .tip {
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
