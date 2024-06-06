<template>
  <div class="panel-wrapper" :class="{ 'is-mobile': state.isMobile }" v-if="state.imgLoaded">
    <div class="container">
      <div class="top-left" ref="cardRef1">
        <Social />
      </div>
      <div class="top-right" ref="cardRef2">
        <Time />
      </div>
      <div class="center" ref="cardRef3">
        <Profile />
      </div>
      <div class="bottom-left" ref="cardRef4">
        <Hitokoto />
      </div>
      <div class="bottom-right" ref="cardRef5">
        <External />
      </div>
    </div>
  </div>
</template>

<script setup>
import { inject } from 'vue'
import Profile from './Profile.vue'
import Hitokoto from './Hitokoto.vue'
import Time from './Time.vue'
import Social from './Social.vue'
import External from './External.vue'
import { useLightCard } from './hook'

const state = inject('state')

const { cardRef: cardRef1 } = useLightCard()
const { cardRef: cardRef4 } = useLightCard()
const { cardRef: cardRef5 } = useLightCard()
const { cardRef: cardRef2 } = useLightCard({
  light: {
    color: '#ffffff',
    width: 100,
  },
})
const { cardRef: cardRef3 } = useLightCard({
  light: {
    color: 'yellow',
  },
})
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
  padding: 10rem;
  transform: scale(0.6);
  transition: transform 0.3s;
  animation: fade-blur-main-in 0.7s cubic-bezier(0.22, 0.97, 0.45, 0.94) forwards;
  animation-delay: 1.1s;
  z-index: 2;
}
.container {
  display: grid;
  justify-content: center;
  align-items: center;
  grid-template-columns: 12rem 10rem 10rem 12rem;
  grid-template-rows: 12rem 10rem 10rem 12rem;
  gap: 10px;
  width: 100%;
  // height: 100vh;
  margin: 0 auto;
  padding: 7rem 0;
  overflow: auto;
  & > div {
    width: 100%;
    height: 100%;
  }
  .top-left {
    grid-area: 1 / 1 / 4 / 2;
  }
  .top-right {
    grid-area: 1 / 2 / 2 / 5;
  }
  .center {
    grid-area: 2 / 2 / 4 / 4;
  }
  .bottom-left {
    grid-area: 4 / 1 / 5 / 4;
  }
  .bottom-right {
    grid-area: 2 / 4 / 5 / 5;
  }
}
</style>
