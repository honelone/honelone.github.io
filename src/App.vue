<template>
  <!-- 加载 -->
  <Loading />
  <!-- 壁纸 -->
  <Background @loadComplete="loadComplete" />
  <Transition name="fade" mode="out-in">
    <header>
      <img alt="Vue logo" class="logo" src="./assets/logo.svg" width="125" height="125" />
    </header>
  </Transition>
</template>

<script setup>
import { watch, nextTick, onMounted, onBeforeUnmount } from 'vue'
import Loading from '@/components/Loading.vue'
import Background from '@/components/Background.vue'
import { mainStore } from '@/stores'
import { helloInit, checkDays } from '@/utils/getTime.js'

const store = mainStore()

// 监听宽度变化
watch(
  () => store.innerWidth,
  (value) => {
    if (value < 990) {
      store.boxOpenState = false
    }
  },
)
// 页面宽度
const getWidth = () => {
  store.setInnerWidth(window.innerWidth)
}

// 加载完成事件
const loadComplete = () => {
  nextTick(() => {
    // 欢迎提示
    helloInit()
    // 默哀模式
    checkDays()
  })
}

onMounted(() => {
  // 鼠标中键事件
  window.addEventListener('mousedown', (event) => {
    if (event.button == 1) {
      store.backgroundShow = !store.backgroundShow
      console.log({
        message: `已${store.backgroundShow ? '开启' : '退出'}壁纸展示状态`,
        grouping: true,
      })
    }
  })

  // 监听当前页面宽度
  getWidth()
  window.addEventListener('resize', getWidth)
})

onBeforeUnmount(() => {
  window.removeEventListener('resize', getWidth)
})
</script>
