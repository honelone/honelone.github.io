<template>
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
</template>

<script setup>
import CustomIcon from '@/components/Icon/CustomIcon.vue'
const externalList = [
  { title: 'Github', icon: 'github', link: 'https://github.com/honelone' },
  { title: 'Juejin', icon: 'juejin', link: 'https://juejin.cn/user/3236585798371246' },
  { title: 'Blog', icon: 'blog', link: 'https://honelone.github.io/note/' },
  { title: 'Pages', icon: 'external', link: 'https://honelone.github.io/pages/' },
]

const handleLink = (link) => {
  if (link) {
    window.open(link)
  }
}
</script>

<style scoped lang="less">
.external {
  display: flex;
  justify-content: space-between;
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
</style>
