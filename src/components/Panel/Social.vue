<template>
  <div class="social custom-card">
    <div class="social-item" v-for="(item, index) in socialList" :key="index">
      <component :is="item.icon" />
      {{ item.title }}
    </div>
  </div>
</template>

<script setup>
import IconGithub from '@/components/Icon/IconGithub.vue'
import IconJuejin from '@/components/Icon/IconJuejin.vue'

const socialList = [
  {
    title: 'Juejin',
    icon: IconJuejin,
  },
  {
    title: 'Github',
    icon: IconGithub,
  },
]
</script>

<style scoped lang="less">
.social {
  .social-item {
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
