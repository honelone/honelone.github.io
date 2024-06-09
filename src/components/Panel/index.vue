<template>
  <div class="panel-wrapper" :class="{ 'is-mobile': state.isMobile }" v-show="state.imgLoaded">
    <div class="perspective-container" ref="perspectiveContainerRef">
      <div class="container">
        <div class="profile">
          <div class="profile-img">
            <img src="@/assets/avatar.png" draggable="false" />
          </div>
          <div class="profile-text">
            <span>Hi, I'm Composition</span>
            <span>Welcome to my page</span>
          </div>
        </div>
        <div class="external">
          <div class="external-item" v-for="(item, index) in externalList" :key="index">
            <CustomIcon :name="item.icon" size="24" />
            {{ item.title }}
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, inject, onMounted } from 'vue'
import CustomIcon from '@/components/Icon/CustomIcon.vue'

const state = inject('state')

const externalList = [
  { title: 'Juejin', icon: 'juejin' },
  { title: 'Github', icon: 'github' },
  { title: 'Blog', icon: 'blog' },
  { title: 'Pages', icon: 'external' },
]

const perspectiveContainerRef = ref(null)
const maxRotate = 10
const rotateY = ref(0)
const rotateX = ref(0)
const radialX = ref(0)
const radialY = ref(0)
onMounted(() => {
  perspectiveContainerRef.value.addEventListener('mousemove', (e) => {
    // console.log('e: ', perspectiveContainerRef.value.getBoundingClientRect())
    const { width, height, left, top } = perspectiveContainerRef.value.getBoundingClientRect()
    const centerX = width / 2
    const centerY = height / 2
    const offsetX = e.clientX - left
    const offsetY = e.clientY - top

    rotateY.value = (maxRotate * (offsetX - centerX)) / centerX
    rotateX.value = ((maxRotate * (offsetY - centerY)) / centerY) * -1

    radialX.value = offsetX
    radialY.value = offsetY
  })
  // window.addEventListener('mousemove', updateMouseReflection)
  perspectiveContainerRef.value.addEventListener('mouseleave', () => {
    rotateY.value = 0
    rotateX.value = 0
    radialX.value = -100
    radialY.value = -100
  })

  window.ondevicemotion = (event) => {
    var accelerationX = event.accelerationIncludingGravity.x
    var accelerationY = event.accelerationIncludingGravity.y
    var accelerationZ = event.accelerationIncludingGravity.z
    // console.log(`${accelerationX},${accelerationY},${accelerationZ}`)
    let xDeg = accelerationX / 10
    let yDeg = accelerationY / 10

    updateMouseReflection(yDeg * 180, xDeg * 100)
    rotateY.value = yDeg * maxRotate
    rotateX.value = xDeg * maxRotate
  }
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
  perspective: 30em;
}
.perspective-container {
  border-radius: 12px;
  transition: all 0.3s ease-out;
  transform: rotateX(calc(v-bind(rotateX) * 1deg)) rotateY(calc(v-bind(rotateY) * 1deg));
}
.container {
  transform-style: preserve-3d;
  position: relative;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  gap: 24px;
  margin: 0 auto;
  overflow: auto;
  padding: 24px;
  border-radius: 12px;
  background-color: #00000050;
  backdrop-filter: blur(12px);
  user-select: none;
  transition: all 0.3s ease-out;
  box-shadow: 20px 20px 75px rgba(0, 0, 0, 0.5);

  background-image: radial-gradient(
    circle at calc(v-bind(radialX) * 1px) calc(v-bind(radialY) * 1px),
    #aaaaaa55,
    transparent
  );

  .profile {
    display: flex;
    justify-content: center;
    align-items: center;
    gap: 24px;
    width: 30rem;
    // height: 20rem;
    .profile-img {
      position: relative;
      display: flex;
      justify-content: center;
      width: 6rem;
      height: 6rem;
      border: 4px solid #f6ede4;
      border-radius: 50%;
      overflow: hidden;
      img {
        width: 100%;
        -webkit-user-drag: none; // 防止图片拖拽的另一种方法，和标签上的 draggable="false" 效果一致
      }
    }
    .profile-text {
      display: flex;
      flex-direction: column;
      gap: 4px;
      font-size: 2rem;
      font-weight: bold;
      pointer-events: none;
      filter: opacity(0.7);
      span {
        transform: translateZ(1px);
        text-shadow: 0 0 4px rgba(0, 0, 0, 0.15);
        background: linear-gradient(45deg, #f5576c 10%, #fee140 100%);
        background-clip: text;
        -webkit-background-clip: text;
        -webkit-text-fill-color: transparent;
      }
    }
  }

  .external {
    display: flex;
    flex-direction: row;
    justify-content: space-between;
    padding: 24px;
    width: 100%;
    .external-item {
      display: flex;
      flex-direction: column;
      align-items: center;
      gap: 4px;
      font-size: 0.7rem;
      color: #fff;
      cursor: pointer;
      transition: all 0.3s;
      &:hover {
        transform: scale(1.05);
        svg {
          fill: #4facfe;
        }
        color: #4facfe;
      }
    }
  }
}
</style>
