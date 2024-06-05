<template>
  <Transition name="fade" mode="out-in">
    <div class="panel-wrapper" :class="{ 'is-mobile': state.isMobile }" v-if="state.imgLoaded">
      <div class="container">
        <Profile />
        <Hitokoto />
        <Time />
      </div>
    </div>
  </Transition>
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
  width: 100%;
  height: 100%;
  transform: scale(1.2);
  transition: transform 0.3s;
  animation: fade-blur-main-in 0.65s cubic-bezier(0.25, 0.46, 0.45, 0.94) forwards;
  animation-delay: 0.5s;
  z-index: 2;
  overflow: auto;
  padding: 7rem 0;
  &.is-mobile {
    color: red;
  }
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
}
</style>
