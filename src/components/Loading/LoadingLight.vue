<template>
  <div class="loading-rotate">
    <div class="loading-rotate-item"></div>
  </div>
</template>
<style lang="less" scoped>
.loading-rotate {
  position: absolute;
  margin: auto;
  z-index: 999;
  display: flex;
  justify-content: center;
  align-items: center;
  width: 150px;
  height: 150px;
  background-color: #d3d3d3;
  border-radius: 50%;
  animation: rotateAnimation 0.8s linear infinite;
  &::before {
    content: '';
    position: absolute;
    top: 0;
    left: 0;
    width: 50%;
    height: 100%;
    background-image: -webkit-linear-gradient(top, #00b9ff, transparent);
    border-top-left-radius: 120px;
    border-bottom-left-radius: 120px;
    animation: colorAnimation 5s linear infinite;
  }
  &::after {
    content: '';
    position: absolute;
    top: -6px;
    width: 12px;
    height: 12px;
    border-radius: 50%;
    background-color: #00b9ff;
    box-shadow: 0 0 5px #00b9ff, 0 0 10px #00b9ff, 0 0 15px #00b9ff, 0 0 25px #00b9ff;
    animation: colorAnimation 5s linear infinite;
  }
  .loading-rotate-item {
    position: relative;
    width: 151px;
    height: 151px;
    background-color: #00305a;
    // background-color: transparent;
    border-radius: 50%;
  }
}
@keyframes rotateAnimation {
  from {
    transform: rotate(0);
  }
  to {
    transform: rotate(360deg);
  }
}
@keyframes colorAnimation {
  from {
    filter: hue-rotate(0) blur(2px);
  }
  to {
    filter: hue-rotate(360deg) blur(2px);
  }
}
</style>
