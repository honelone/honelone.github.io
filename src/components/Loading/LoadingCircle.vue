<template>
  <div class="loading-rotate"></div>
</template>
<style lang="less" scoped>
.loading-rotate {
  position: absolute;
  margin: auto;
  z-index: 999;
  width: 150px;
  height: 150px;
  border-radius: 50%;
  border-top: 10px solid #fbc2eb;
  animation: rotateAnimation 1.5s linear infinite;
  &::before,
  &::after {
    content: '';
    position: absolute;
    top: -10px;
    left: 0;
    width: 100%;
    height: 100%;
    border-radius: 50%;
  }
  &::before {
    border-top: 10px solid #a18cd1;
    transform: rotate(120deg);
  }
  &::after {
    border-bottom: 10px solid #8fd3f4;
    transform: rotate(60deg);
  }
}
</style>
