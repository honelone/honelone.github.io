<template>
  <div class="external">
    <div class="external-item" v-for="(item, index) in externalList" :key="index">
      <component :is="item.icon" />
      {{ item.title }}
    </div>
  </div>
</template>

<script setup>
import IconGithub from '@/components/Icon/IconGithub.vue'
import IconJuejin from '@/components/Icon/IconJuejin.vue'
import IconBlog from '@/components/Icon/IconBlog.vue'
import IconExternal from '@/components/Icon/IconExternal.vue'

const externalList = [
  {
    title: 'Juejin',
    icon: IconJuejin,
  },
  {
    title: 'Github',
    icon: IconGithub,
  },
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
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  padding: 24px;
  .external-item {
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 4px;
    font-size: 1.2rem;
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
