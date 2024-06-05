<template>
  <!-- 功能区域 -->
  <div :class="state.isMobile ? 'function mobile' : 'function'">
    <div class="right cards">
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
      <Weather />
    </div>
  </div>
</template>

<script setup>
import { ref, inject, onMounted, onBeforeUnmount } from 'vue'
import { getCurrentTime } from '@/utils/getTime'
import Weather from '@/components/Panel/Weather.vue'

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
.function {
  display: flex;
  flex-direction: row;
  align-items: center;
  justify-content: space-between;

  &.mobile {
  }

  .right {
    padding: 20px;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: space-between;
    animation: fadeAnimation 0.5s;

    .time {
      font-size: 1.1rem;
      text-align: center;

      .date {
        text-overflow: ellipsis;
        overflow-x: hidden;
        white-space: nowrap;
      }

      .text {
        margin-top: 10px;
        font-size: 3.25rem;
        letter-spacing: 2px;
        font-family: 'UnidreamLED';
      }
    }

    .weather {
      text-align: center;
      width: 100%;
      text-overflow: ellipsis;
      overflow-x: hidden;
      white-space: nowrap;
    }
  }
}
</style>
