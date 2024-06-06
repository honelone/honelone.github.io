<template>
  <div class="external custom-card">
    <div class="external-item" v-for="(item, index) in externalList" :key="index">
      <component :is="item.icon" />
      {{ item.title }}
    </div>
  </div>
</template>

<script setup>
import IconBlog from '@/components/Icon/IconBlog.vue'
import IconExternal from '@/components/Icon/IconExternal.vue'

const externalList = [
  {
    title: 'Blog',
    icon: IconBlog,
  },
  {
    title: 'Pages',
    icon: IconExternal,
  },
]
</script>

<style scoped lang="less">
.external {
  .external-item {
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 12px;
    font-size: 1.5rem;
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
