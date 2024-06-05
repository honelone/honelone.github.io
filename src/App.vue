<template>
  <!-- 加载 -->
  <Loading />
  <!-- 壁纸 -->
  <Background />
  <!-- 内容 -->
  <Panel />
</template>

<script setup>
import { reactive, watch, provide, nextTick, onMounted, onBeforeUnmount } from 'vue'
import Loading from '@/components/Loading/index.vue'
import Background from '@/components/Background/index.vue'
import Panel from '@/components/Panel/index.vue'

const state = reactive({
  isMobile: false,
  coverType: '0',
  innerWidth: 0,
  setInnerWidth: (value) => {
    state.innerWidth = value
    if (value >= 720) {
      state.isMobile = false
    } else {
      state.isMobile = true
    }
  },
  imgLoaded: false,
  setImgLoaded: (value) => {
    state.imgLoaded = value
  },
})
provide('state', state)

const handleResize = () => {
  state.setInnerWidth(window.innerWidth)
}
onMounted(() => {
  handleResize()
  window.addEventListener('resize', handleResize)
})
onBeforeUnmount(() => {
  window.removeEventListener('resize', handleResize)
})
</script>
