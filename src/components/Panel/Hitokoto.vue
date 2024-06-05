<template>
  <div class="hitokoto custom-card" @click.stop>
    <Transition name="el-fade-in-linear" mode="out-in">
      <div :key="hitokotoData.text" class="content" @click="handleUpdate">
        <span class="text">{{ hitokotoData.text }}</span>
        <span class="from">-「&nbsp;{{ hitokotoData.from }}&nbsp;」</span>
      </div>
    </Transition>
  </div>
</template>

<script setup>
import { ref, reactive, onMounted } from 'vue'

// 一言数据
const hitokotoData = reactive({ text: '', from: '' })

// 获取一言数据
const isFetching = ref(false)
const getHitokotoData = async () => {
  if (isFetching.value) return
  try {
    isFetching.value = true
    const response = await fetch('https://v1.hitokoto.cn')
    const { hitokoto, from } = await response.json()
    hitokotoData.text = hitokoto
    hitokotoData.from = from
  } catch (error) {
    hitokotoData.text = '这里应该显示一句话这里应该显示一句话'
    hitokotoData.from = '無名'
  } finally {
    setTimeout(() => {
      isFetching.value = false
    }, 1000)
  }
}

// 更新一言数据
const handleUpdate = () => {
  getHitokotoData()
}

onMounted(() => {
  getHitokotoData()
})
</script>

<style lang="less" scoped>
.hitokoto {
  .open-music {
    width: 100%;
    position: absolute;
    top: 0;
    left: 0;
    display: flex;
    align-items: center;
    justify-content: center;
    background: #00000026;
    padding: 4px 0;
    border-radius: 8px 8px 0 0;

    .i-icon {
      width: 18px;
      height: 18px;
      display: block;
      margin-right: 8px;
    }

    span {
      font-size: 0.95rem;
    }
  }

  .content {
    height: 100%;
    display: flex;
    flex-direction: column;
    justify-content: space-evenly;

    .text {
      font-size: 1.1rem;
      word-break: break-all;
      text-overflow: ellipsis;
      overflow: hidden;
      display: -webkit-box;
      -webkit-line-clamp: 3;
      -webkit-box-orient: vertical;
    }

    .from {
      margin-top: 10px;
      font-weight: bold;
      align-self: flex-end;
      font-size: 1.1rem;
    }
  }
}
</style>
