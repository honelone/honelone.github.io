<template>
  <div class="time">
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
import { ref, onMounted, onBeforeUnmount } from 'vue'
import { getCurrentTime } from '@/utils/time'

// 当前时间
const currentTime = ref({})
const timeInterval = ref(null)

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
  display: flex;
  align-items: center;
  gap: 12px;
  margin-bottom: 12px;
  .date {
    text-overflow: ellipsis;
    overflow-x: hidden;
    white-space: nowrap;
  }

  .text {
    letter-spacing: 2px;
  }
}
</style>
