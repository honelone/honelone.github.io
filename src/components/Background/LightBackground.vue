<template>
  <div class="light-background-wrapper">
    <div class="light x1"></div>
    <div class="light x2"></div>
    <div class="light x3"></div>
    <div class="light x4"></div>
    <div class="light x5"></div>
    <div class="light x6"></div>
    <div class="light x7"></div>
    <div class="light x8"></div>
    <div class="light x9"></div>
  </div>
</template>
<style scoped lang="less">
.light-background-wrapper {
  margin: 0;
  height: 100vh;
  font-weight: 100;
  background: radial-gradient(#8ec5fc, transparent);
  overflow-y: hidden;
}
.light {
  position: absolute;
  top: 100vh;
  bottom: 0;
  left: 0;
  right: 0;
  width: 0;
  background-color: white;
  box-shadow: #e9f1f1 0px 0px 20px 2px;
  opacity: 0;
  margin: auto;
}

.x1 {
  animation: floatUp 4s infinite linear;
  transform: scale(1);
}

.x2 {
  animation: floatUp 7s infinite linear;
  transform: scale(1.6);
  left: 15%;
}

.x3 {
  animation: floatUp 2.5s infinite linear;
  transform: scale(0.5);
  left: -15%;
}

.x4 {
  animation: floatUp 4.5s infinite linear;
  transform: scale(1.2);
  left: -34%;
}

.x5 {
  animation: floatUp 8s infinite linear;
  transform: scale(2.2);
  left: -57%;
}

.x6 {
  animation: floatUp 3s infinite linear;
  transform: scale(0.8);
  left: -81%;
}

.x7 {
  animation: floatUp 5.3s infinite linear;
  transform: scale(3.2);
  left: 37%;
}

.x8 {
  animation: floatUp 4.7s infinite linear;
  transform: scale(1.7);
  left: 62%;
}

.x9 {
  animation: floatUp 4.1s infinite linear;
  transform: scale(0.9);
  left: 85%;
}

@keyframes floatUp {
  0% {
    top: 100vh;
    opacity: 0;
  }
  25% {
    opacity: 1;
  }
  50% {
    top: 0vh;
    opacity: 0.8;
  }
  75% {
    opacity: 1;
  }
  100% {
    top: -100vh;
    opacity: 0;
  }
}
</style>
