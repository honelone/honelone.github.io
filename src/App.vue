<template>
  <!-- 加载 -->
  <Loading />
  <!-- 壁纸 -->
  <Background @loadComplete="loadComplete" />
  <Transition name="fade" mode="out-in">
    <main id="main" v-if="store.imgLoadStatus">
      <div class="container" v-show="!store.backgroundShow">
        <Hitokoto />
        <TimePanel />
      </div>
    </main>
  </Transition>
</template>

<script setup>
import { watch, nextTick, onMounted, onBeforeUnmount } from 'vue'
import { mainStore } from '@/stores'
import { helloInit, checkDays } from '@/utils/getTime.js'
import Loading from '@/components/Loading.vue'
import Background from '@/components/Background.vue'
import Hitokoto from '@/components/Hitokoto.vue'
import TimePanel from '@/components/TimePanel.vue'

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

<style lang="less" scoped>
.container {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  gap: 24px;
  width: 100%;
  // height: 100vh;
  margin: 0 auto;
}
</style>
