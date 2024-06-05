<template>
  <div
    class="hitokoto cards"
    @mouseenter="openMusicShow = true"
    @mouseleave="openMusicShow = false"
    @click.stop
  >
    <!-- 一言内容 -->
    <Transition name="el-fade-in-linear" mode="out-in">
      <div :key="hitokotoData.text" class="content" @click="updateHitokoto">
        <span class="text">{{ hitokotoData.text }}</span>
        <span class="from">-「&nbsp;{{ hitokotoData.from }}&nbsp;」</span>
      </div>
    </Transition>
  </div>
</template>

<script setup>
import { ref, reactive, onMounted } from 'vue'
import { getHitokoto } from '@/api'

// 开启音乐面板按钮显隐
const openMusicShow = ref(false)

// 一言数据
const hitokotoData = reactive({
  text: '这里应该显示一句话',
  from: '無名',
})

// 获取一言数据
const getHitokotoData = async () => {
  try {
    const result = await getHitokoto()
    hitokotoData.text = result.hitokoto
    hitokotoData.from = result.from
  } catch (error) {
    console.error({
      message: '一言获取失败',
    })
    hitokotoData.text = '这里应该显示一句话'
    hitokotoData.from = '無名'
  }
}

// 更新一言数据
const updateHitokoto = () => {
  // 防抖
  getHitokotoData()
}

onMounted(() => {
  getHitokotoData()
})
</script>

<style lang="less" scoped>
.hitokoto {
  // width: 100%;
  // height: 100%;
  padding: 20px;
  animation: fadeAnimation 0.5s;

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
