<template>
  <div v-show="state.imgLoaded" class="panel-wrapper" :class="{ 'is-mobile': state.isMobile }">
    <div ref="perspectiveContainerRef" class="perspective-container">
      <div ref="containerRef" class="container">
        <div class="profile">
          <div class="profile-img">
            <img src="@/assets/avatar.png" draggable="false" />
          </div>
          <div class="profile-text colorful">Hi, I'm Composition</div>
          <div class="profile-text">Welcome to my page</div>
        </div>
        <div class="external">
          <div
            class="external-item"
            v-for="(item, index) in externalList"
            :key="index"
            @click="handleLink(item.link)"
          >
            <CustomIcon :name="item.icon" size="36" />
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
  { title: 'Github', icon: 'github', link: 'https://github.com/honelone' },
  { title: 'Juejin', icon: 'juejin', link: '' },
  { title: 'Blog', icon: 'blog', link: 'https://honelone.github.io/note/' },
  { title: 'Pages', icon: 'external', link: 'https://honelone.github.io/pages/' },
]
const handleLink = (link) => {
  if (link) {
    window.open(link)
  }
}

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
        box-shadow: 20px 20px 75px #00000080;
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
      background-color: #00000040;
      backdrop-filter: blur(12px);
      user-select: none;
      pointer-events: all;

      transition: all 0.3s ease-out;
      transform-style: preserve-3d;
      transform: rotateX(calc(v-bind(rotateX) * 1deg)) rotateY(calc(v-bind(rotateY) * 1deg));
      background-image: radial-gradient(
        circle at calc(v-bind(radialX) * 1px) calc(v-bind(radialY) * 1px),
        #ffffff50,
        transparent
      );

      .profile {
        display: flex;
        justify-content: center;
        align-items: center;
        flex-direction: column;
        gap: 12px;
        width: 24rem;
        // height: 20rem;
        z-index: 9;
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
          text-shadow: 1px 1px 1px #000, -1px -1px 1px #fff;

          &.colorful {
            text-shadow: none;
            background: -webkit-linear-gradient(315deg, #01e5f7 10%, #2f1eb9 50%, #68e8d8 90%);
            background-clip: text;
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-size: 400% 400%;
            animation: gradientAnimation 20s -10s ease infinite;
          }
        }
      }

      .external {
        display: flex;
        justify-content: space-around;
        width: 100%;
        z-index: 9;
        .external-item {
          display: flex;
          flex-direction: column;
          align-items: center;
          gap: 4px;
          font-size: 1rem;
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
  }
  &.is-mobile {
    padding: 1rem;
    height: 80%;
    .perspective-container {
      .container {
        width: 100%;
        height: 100%;
        overflow: scroll;
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
}
</style>
