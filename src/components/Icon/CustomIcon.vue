<template>
  <component class="custom-icon" :is="curIcon" />
</template>

<script setup>
import { computed } from 'vue'
import IconGithub from './IconGithub.vue'
import IconJuejin from './IconJuejin.vue'
import IconBlog from './IconBlog.vue'
import IconExternal from './IconExternal.vue'

const props = defineProps({
  name: { type: String },
  size: { type: [Number, String], required: false, default: 16 },
  color: { type: String, required: false, default: '#fff' },
})
const sizeState = computed(() => {
  return {
    width: props.size + 'px',
    height: props.size + 'px',
  }
})

const curIcon = computed(() => {
  switch (props.name) {
    case 'github':
      return IconGithub
    case 'juejin':
      return IconJuejin
    case 'blog':
      return IconBlog
    case 'external':
      return IconExternal
    default:
      return null
  }
})
</script>

<style scoped lang="less">
.custom-icon {
  cursor: pointer;
  transition: fill 0.3s;
  width: v-bind('sizeState.width');
  height: v-bind('sizeState.height');
  fill: v-bind('props.color');
}
</style>
