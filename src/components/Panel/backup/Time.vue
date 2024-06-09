<template>
  <div class="time custom-card">
    <div class="date">
      <span>{{ currentTime.year }}&nbsp;年&nbsp;</span>
      <span>{{ currentTime.month }}&nbsp;月&nbsp;</span>
      <span>{{ currentTime.day }}&nbsp;日&nbsp;</span>
      <span class="sm-hidden">{{ currentTime.weekday }}</span>
    </div>
    <div class="text">
      <span> {{ currentTime.hour }}:{{ currentTime.minute }}:{{ currentTime.second }}</span>
    </div>
  </div>
</template>

<script setup>
import { ref, inject, onMounted, onBeforeUnmount } from 'vue'
import { getCurrentTime } from '@/utils/getTime'

const state = inject('state')

// 当前时间
const currentTime = ref({})
const timeInterval = ref(null)

// 播放器 id
const playerHasId = import.meta.env.VITE_SONG_ID

// 更新时间
const updateTimeData = () => {
  currentTime.value = getCurrentTime()
}

onMounted(() => {
  updateTimeData()
  timeInterval.value = setInterval(updateTimeData, 1000)
})

onBeforeUnmount(() => {
  clearInterval(timeInterval.value)
})
</script>

<style lang="less" scoped>
.time {
  font-size: 2rem;

  .date {
    text-overflow: ellipsis;
    overflow-x: hidden;
    white-space: nowrap;
  }

  .text {
    font-size: 3rem;
    letter-spacing: 2px;
  }
}
</style>
