<template>
  <div class="filter-background-wrapper">
    <span v-for="i in 20" :key="i"></span>
  </div>
</template>

<script setup></script>

<style scoped lang="less">
.filter-background-wrapper {
  width: 100vw;
  height: 100vh;
  background: #537895;
  span {
    width: 20vmin;
    height: 20vmin;
    border-radius: 20vmin;
    backface-visibility: hidden;
    position: absolute;
    animation-name: move;
    animation-duration: 6s;
    animation-timing-function: linear;
    animation-iteration-count: infinite;

    &:nth-child(1) {
      color: #e3fdf5;
      top: 47%;
      left: 10%;
      animation-duration: 10.5s;
      animation-delay: -12.6s;
      transform-origin: 0vw -9vh;
      box-shadow: -40vmin 0 11.2034042917vmin currentColor;
    }
    &:nth-child(2) {
      color: #8ec5fc;
      top: 33%;
      left: 45%;
      animation-duration: 13.2s;
      animation-delay: -15.6s;
      transform-origin: 14vw 17vh;
      box-shadow: 40vmin 0 10.2115006212vmin currentColor;
    }
    &:nth-child(3) {
      color: #00f2fe;
      top: 90%;
      left: 55%;
      animation-duration: 14.8s;
      animation-delay: -3.5s;
      transform-origin: -18vw 9vh;
      box-shadow: -40vmin 0 12.3544421218vmin currentColor;
    }
    &:nth-child(4) {
      color: #f9fea5;
      top: 7%;
      left: 88%;
      animation-duration: 15.4s;
      animation-delay: -2.6s;
      transform-origin: 21vw 14vh;
      box-shadow: -40vmin 0 5.9226682716vmin currentColor;
    }
    &:nth-child(5) {
      color: #38f9d7;
      top: 65%;
      left: 26%;
      animation-duration: 15.3s;
      animation-delay: -6s;
      transform-origin: 9vw -23vh;
      box-shadow: 40vmin 0 5.4289289226vmin currentColor;
    }
    &:nth-child(6) {
      color: #30cfd0;
      top: 45%;
      left: 30%;
      animation-duration: 11.2s;
      animation-delay: -6.6s;
      transform-origin: -3vw 23vh;
      box-shadow: -40vmin 0 14.4480182393vmin currentColor;
    }
    &:nth-child(7) {
      color: #7de2fc;
      top: 40%;
      left: 95%;
      animation-duration: 10.3s;
      animation-delay: -6.6s;
      transform-origin: 6vw 1vh;
      box-shadow: -40vmin 0 5.2476920034vmin currentColor;
    }
    &:nth-child(8) {
      color: #e4efe9;
      top: 84%;
      left: 91%;
      animation-duration: 15.6s;
      animation-delay: -15.3s;
      transform-origin: 15vw 20vh;
      box-shadow: 40vmin 0 5.328532637vmin currentColor;
    }
    &:nth-child(9) {
      color: #00ecbc;
      top: 88%;
      left: 49%;
      animation-duration: 12.5s;
      animation-delay: -6.3s;
      transform-origin: -23vw 17vh;
      box-shadow: -40vmin 0 13.7564470826vmin currentColor;
    }
    &:nth-child(10) {
      color: #66a6ff;
      top: 4%;
      left: 16%;
      animation-duration: 11.9s;
      animation-delay: -10.2s;
      transform-origin: -4vw 13vh;
      box-shadow: 40vmin 0 13.95746731vmin currentColor;
    }
    &:nth-child(11) {
      color: #96deda;
      top: 16%;
      left: 99%;
      animation-duration: 10.4s;
      animation-delay: -9s;
      transform-origin: -3vw -5vh;
      box-shadow: -40vmin 0 11.6603526433vmin currentColor;
    }
    &:nth-child(12) {
      color: #009efd;
      top: 46%;
      left: 81%;
      animation-duration: 11.4s;
      animation-delay: -9.2s;
      transform-origin: 3vw -1vh;
      box-shadow: -40vmin 0 14.0594399762vmin currentColor;
    }
    &:nth-child(13) {
      color: #2575fc;
      top: 69%;
      left: 75%;
      animation-duration: 12.3s;
      animation-delay: -7.7s;
      transform-origin: 13vw -4vh;
      box-shadow: -40vmin 0 14.688619748vmin currentColor;
    }
    &:nth-child(14) {
      color: #72afd3;
      top: 67%;
      left: 52%;
      animation-duration: 12.3s;
      animation-delay: -1.2s;
      transform-origin: 23vw -5vh;
      box-shadow: -40vmin 0 13.6204973407vmin currentColor;
    }
    &:nth-child(15) {
      color: #6f86d6;
      top: 38%;
      left: 57%;
      animation-duration: 12.4s;
      animation-delay: -8.2s;
      transform-origin: 11vw 19vh;
      box-shadow: 40vmin 0 13.6934527314vmin currentColor;
    }
    &:nth-child(16) {
      color: #e7f0fd;
      top: 78%;
      left: 94%;
      animation-duration: 13.4s;
      animation-delay: -13.2s;
      transform-origin: -19vw 8vh;
      box-shadow: -40vmin 0 8.3807133847vmin currentColor;
    }
    &:nth-child(17) {
      color: #00c6fb;
      top: 57%;
      left: 38%;
      animation-duration: 15.5s;
      animation-delay: -12.1s;
      transform-origin: -21vw -20vh;
      box-shadow: -40vmin 0 10.8162910663vmin currentColor;
    }
    &:nth-child(18) {
      color: #6991c7;
      top: 65%;
      left: 45%;
      animation-duration: 11.2s;
      animation-delay: -2.6s;
      transform-origin: 0vw -22vh;
      box-shadow: -40vmin 0 8.9038134634vmin currentColor;
    }
    &:nth-child(19) {
      color: #495aff;
      top: 18%;
      left: 39%;
      animation-duration: 11.7s;
      animation-delay: -15.9s;
      transform-origin: -24vw 11vh;
      box-shadow: 40vmin 0 7.2048026951vmin currentColor;
    }
    &:nth-child(20) {
      color: #0acffe;
      top: 87%;
      left: 15%;
      animation-duration: 11.1s;
      animation-delay: -6.2s;
      transform-origin: -9vw -24vh;
      box-shadow: -40vmin 0 12.9500645493vmin currentColor;
    }
  }
}

@keyframes move {
  100% {
    transform: translate3d(0, 0, 1px) rotate(360deg);
  }
}
</style>
