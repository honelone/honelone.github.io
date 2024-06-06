<template>
  <div class="panel-wrapper" :class="{ 'is-mobile': state.isMobile }" v-if="state.imgLoaded">
    <div class="container">
      <Profile />
      <Hitokoto />
      <Time />
      <div>123</div>
    </div>
  </div>
</template>

<script setup>
import { inject } from 'vue'
import Profile from './Profile.vue'
import Hitokoto from './Hitokoto.vue'
import Time from './Time.vue'

const state = inject('state')
</script>

<style scoped lang="less">
.panel-wrapper {
  position: absolute;
  top: 0;
  left: 0;
  display: flex;
  align-items: center;
  justify-content: center;
  width: 100%;
  height: 100%;
  transform: scale(0.6);
  transition: transform 0.3s;
  animation: fade-blur-main-in 0.7s cubic-bezier(0.22, 0.97, 0.45, 0.94) forwards;
  animation-delay: 1.1s;
  z-index: 2;
}
.container {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  gap: 24px;
  width: 100%;
  // height: 100vh;
  margin: 0 auto;
  padding: 7rem 0;
  overflow: auto;
}
</style>
