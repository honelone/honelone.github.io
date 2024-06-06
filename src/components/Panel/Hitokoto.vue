<template>
  <div class="hitokoto custom-card" @click="handleUpdate">
    <span class="text">{{ currentData.text }}</span>
    <span class="from">—— {{ currentData.from }}</span>
  </div>
</template>

<script setup>
import { ref, reactive, onMounted } from 'vue'

const currentData = reactive({ text: '', from: '' })

const isFetching = ref(false)
const getData = async () => {
  if (isFetching.value) return
  try {
    isFetching.value = true
    const response = await fetch('https://v1.hitokoto.cn')
    const { hitokoto, from } = await response.json()
    currentData.text = hitokoto
    currentData.from = from
  } catch (error) {
    currentData.text = '这里应该显示一句话这里应该显示一句话'
    currentData.from = '無名'
  } finally {
    setTimeout(() => {
      isFetching.value = false
    }, 1000)
  }
}

const handleUpdate = () => {
  getData()
}

onMounted(() => {
  getData()
})
</script>

<style lang="less" scoped>
.hitokoto {
  font-size: 1.5rem;
  .text {
    word-break: break-all;
    text-overflow: ellipsis;
    overflow: hidden;
    display: -webkit-box;
    -webkit-line-clamp: 2;
    -webkit-box-orient: vertical;
  }

  .from {
    margin-top: 10px;
    font-weight: bold;
    align-self: flex-end;
  }
}
</style>
