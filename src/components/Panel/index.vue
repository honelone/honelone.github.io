<template>
  <div v-show="state.imgLoaded" class="panel-wrapper" :class="{ 'is-mobile': state.isMobile }">
    <div ref="perspectiveContainerRef" class="perspective-container">
      <div ref="containerRef" class="container">
        <div class="inner">
          <Profile />
          <div class="inner-right">
            <Time />
            <Weather />
            <Hitokoto />
            <External />
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, inject, onMounted } from 'vue'
import Time from './backup/Time.vue'
import Weather from './backup/Weather.vue'
import Profile from './backup/Profile.vue'
import External from './backup/External.vue'
import Hitokoto from './backup/Hitokoto.vue'

const state = inject('state')

const perspectiveContainerRef = ref(null)
const containerRef = ref(null)
const maxRotate = 20
const rotateY = ref(0)
const rotateX = ref(0)
const radialX = ref(0)
const radialY = ref(0)
onMounted(() => {
  perspectiveContainerRef.value.addEventListener('mousemove', (e) => {
    // console.log('e: ', perspectiveContainerRef.value.getBoundingClientRect())
    const { width, height, left, top } = containerRef.value.getBoundingClientRect()
    const centerX = width / 2
    const centerY = height / 2
    const offsetX = e.clientX - left
    const offsetY = e.clientY - top

    window.requestAnimationFrame(() => {
      rotateY.value = ((maxRotate * (offsetX - centerX)) / centerX) * -1
      rotateX.value = ((maxRotate * (offsetY - centerY)) / centerY) * 1

      radialX.value = offsetX
      radialY.value = offsetY
    })
  })
  perspectiveContainerRef.value.addEventListener('mouseleave', () => {
    window.requestAnimationFrame(() => {
      rotateY.value = 0
      rotateX.value = 0
      radialX.value = -100
      radialY.value = -100
    })
  })

  perspectiveContainerRef.value.addEventListener('touchmove', (e) => {
    // console.log('e: ', { e, clientX: e.touches[0].clientX, clientY: e.touches[0].clientY })
    e.preventDefault()

    const { width, height, left, top } = containerRef.value.getBoundingClientRect()
    const centerX = width / 2
    const centerY = height / 2
    const offsetX = e.touches[0].clientX - left
    const offsetY = e.touches[0].clientY - top

    window.requestAnimationFrame(() => {
      rotateY.value = ((maxRotate * (offsetX - centerX)) / centerX) * -1
      rotateX.value = ((maxRotate * (offsetY - centerY)) / centerY) * 1

      radialX.value = offsetX
      radialY.value = offsetY
    })
  })
  perspectiveContainerRef.value.addEventListener('touchend', () => {
    window.requestAnimationFrame(() => {
      rotateY.value = 0
      rotateX.value = 0
      radialX.value = -100
      radialY.value = -100
    })
  })
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
  animation: fade-blur-main-in 0.7s cubic-bezier(0.22, 0.97, 0.45, 0.94) forwards;
  animation-delay: 1.1s;
  z-index: 2;
  user-select: none;
  pointer-events: none;
  .perspective-container {
    border-radius: 12px;
    transition: all 0.3s ease-out;
    perspective: 30em;
    &::after {
      position: absolute;
      content: '';
      top: -5rem;
      bottom: -5rem;
      left: -5rem;
      right: -5rem;
    }
    &:hover {
      .container {
        scale: 1.1;
        box-shadow: 20px 20px 75px #00000080;
      }
    }

    .container {
      background-color: #00000040;
      backdrop-filter: blur(12px);
      user-select: none;
      pointer-events: all;

      transition: all 0.3s ease-out;
      transform-style: preserve-3d;
      transform: rotateX(calc(v-bind(rotateX) * 1deg)) rotateY(calc(v-bind(rotateY) * 1deg));
      background-image: radial-gradient(
        circle at calc(v-bind(radialX) * 1px) calc(v-bind(radialY) * 1px),
        #00000070 1%,
        transparent
      );
    }
  }
  &.is-mobile {
    padding: 1rem;
    height: 80%;
    .perspective-container {
      .container {
        width: 100%;
        height: 100%;
        overflow: scroll;
        .inner {
          flex-direction: column;
        }
        .profile {
          flex-direction: column;
          width: 100%;
          height: 100%;
          .profile-text {
            font-size: 1.8rem;
          }
        }
      }
    }
  }
  .container {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    gap: 24px;
    margin: 0 auto;
    overflow: auto;
    padding: 24px;
    border-radius: 12px;
    .inner {
      display: flex;
      gap: 24px;
      .inner-right {
        display: flex;
        flex-direction: column;
        justify-content: space-evenly;
      }
    }
  }
}
</style>
