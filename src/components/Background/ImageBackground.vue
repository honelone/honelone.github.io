<template>
  <div class="image-background-wrapper">
    <img
      v-show="state.imgLoaded"
      class="background-wrapper-bg"
      alt="bgImg"
      :src="bgUrl"
      @load="handleImgLoadSuccess"
      @error.once="handleImgLoadError"
      @animationend="handleImgAnimationEnd"
    />
  </div>
</template>

<script setup>
import { ref, watch, inject, onMounted, onBeforeUnmount } from 'vue'

const state = inject('state')
const emits = defineEmits(['loadComplete'])

const bgRandom = Math.floor(Math.random() * 13 + 1)

// 监听壁纸切换
watch(
  () => state.coverType,
  (value) => {
    handleUpdateImg(value)
  },
)

const bgUrl = ref(null)
const handleUpdateImg = (type) => {
  if (type == 0) {
    bgUrl.value = `/images/bg${bgRandom}.jpg`
  } else if (type == 1) {
    bgUrl.value = 'https://api.dujin.org/bing/1920.php'
  } else if (type == 2) {
    bgUrl.value = 'https://api.aixiaowai.cn/gqapi/gqapi.php'
  } else if (type == 3) {
    bgUrl.value = 'https://api.aixiaowai.cn/api/api.php'
  }
}

const imgTimeout = ref(null)
const handleImgLoadSuccess = () => {
  imgTimeout.value = setTimeout(() => {
    state.setImgLoaded(true)
  }, Math.floor(Math.random() * (600 - 300 + 1)) + 300)
}
const handleImgLoadError = () => {
  bgUrl.value = `/images/bg${bgRandom}.jpg`
}
const handleImgAnimationEnd = () => {
  emits('loadComplete')
}

onMounted(() => {
  handleUpdateImg(state.coverType)
})

onBeforeUnmount(() => {
  clearTimeout(imgTimeout.value)
})
</script>

<style scoped lang="less">
.image-background-wrapper {
  width: 100%;
  height: 100%;

  .background-wrapper-bg {
    position: absolute;
    left: 0;
    top: 0;
    width: 100%;
    height: 100%;
    object-fit: cover;
    backface-visibility: hidden;
    filter: blur(25px) brightness(0.3);
    transition: filter 0.3s, transform 0.3s;
    animation: blurAnimation 0.8s cubic-bezier(0.25, 0.46, 0.45, 0.94) forwards;
    animation-delay: 1.1s;
  }
}
</style>
