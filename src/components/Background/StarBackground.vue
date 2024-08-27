<template>
  <div class="star-background-wrapper">
    <canvas id="canvas" class="canvas"></canvas>
  </div>
</template>

<script lang="ts" setup>
import { ref, onMounted, inject } from 'vue'

const state = inject('state')

const width = ref(0)
const height = ref(0)
const canvas = ref(null)
const ctx = ref()
const gradient = ref()

onMounted(() => {
  get_width()
  generate_stars()
  meteorGenerator()
  requestAnimationFrame(() => {
    draw_all()
  })
  setTimeout(() => {
    state.setImgLoaded(true)
  }, 1000 * 3)
})
// Main
function get_width() {
  width.value = window.innerWidth
  height.value = window.innerHeight
  canvas.value = document.getElementById('canvas')
  ctx.value = canvas.value.getContext('2d')
  canvas.value.width = width.value
  canvas.value.height = height.value
}

function draw_all() {
  ctx.value.clearRect(0, 0, width.value, height.value)
  draw_moon()
  stars_blink()
  draw_star()
  control_meteor()
  requestAnimationFrame(() => {
    draw_all()
  })
}

// Star
let x = new Array(100)
let y = new Array(100)
let r = new Array(100)
function generate_stars() {
  ctx.value.fillStyle = 'white'
  for (let i = 0; i < 200; i++) {
    x[i] = Math.random() * width.value
    y[i] = Math.random() * height.value
    r[i] = Math.random() + 0.2
    ctx.value.beginPath()
    ctx.value.arc(x[i], y[i], r[i], 0, 2 * Math.PI)
    ctx.value.fill()
  }
}
function stars_blink() {
  for (let i = 0; i < 200; i++) {
    let sign = Math.random() > 0.5 ? 1 : -1
    r[i] += sign * 0.2
    if (r[i] < 0) {
      r[i] = -r[i]
    } else if (r[i] > 1) {
      r[i] -= 0.2
    }
  }
}
function draw_star() {
  for (let i = 0; i < 200; i++) {
    ctx.value.fillStyle = 'white'
    ctx.value.beginPath()
    ctx.value.arc(x[i], y[i], r[i], 0, 2 * Math.PI)
    ctx.value.fill()
    ctx.value.closePath()
  }
}

// Moon
function draw_moon() {
  gradient.value = ctx.value.createRadialGradient(200, 200, 80, 200, 200, 800)
  //径向渐变
  gradient.value.addColorStop(0, 'rgb(255,255,255)')
  gradient.value.addColorStop(0.01, 'rgb(70,70,80)')
  gradient.value.addColorStop(0.2, 'rgb(40,40,50)')
  gradient.value.addColorStop(0.4, 'rgb(20,20,30)')
  gradient.value.addColorStop(1, 'rgb(0,0,10)')
  ctx.value.fillStyle = gradient.value
  ctx.value.fillRect(0, 0, width.value, height.value)
}

// Meteor
let meteor_x = []
let meteor_y = []
let meteor_r = []
function meteorGenerator() {
  //x位置偏移，以免经过月亮
  let x_m = Math.random() * width.value + 800
  let r_m = Math.random() * 300 + 500
  meteor_x.push(x_m)
  meteor_r.push(r_m)
  meteor_y.push(0)
  //每隔随机时间，生成新流星
  setTimeout(meteorGenerator, Math.random() * 2000)
}

function flow(i) {
  let va = -(4 + Math.random() * 4)
  let vb = -va
  if (meteor_x[i] < -meteor_r[i] || meteor_y[i] > height.value + meteor_r[i]) {
    return false
  }
  meteor_x[i] += va
  meteor_y[i] += vb
  return true
}

const gra = ref()
function draw_meteor(a, b, c) {
  //径向渐变，从流星头尾圆心，半径越大，透明度越高
  gra.value = ctx.value.createRadialGradient(a, b, 0, a, b, c)

  gra.value.addColorStop(0, 'rgba(230,237,17,1)')
  gra.value.addColorStop(1, 'rgba(0,0,0,0)')
  ctx.value.fillStyle = gra.value
  ctx.value.beginPath()
  //流星头，二分之一圆
  ctx.value.arc(a, b, 1, Math.PI / 4, (5 * Math.PI) / 4)
  //绘制流星尾，三角形
  ctx.value.lineTo(a + c, b - c)
  ctx.value.closePath()
  ctx.value.fill()
}
function control_meteor() {
  for (let i = 0; i < meteor_x.length; i++) {
    if (flow(i)) draw_meteor(meteor_x[i], meteor_y[i], meteor_r[i])
    else {
      meteor_x.splice(i, 1)
      meteor_y.splice(i, 1)
      meteor_r.splice(i, 1)
    }
  }
}
</script>

<style scoped lang="less">
.star-background-wrapper {
  width: 100vw;
  height: 100vh;
  .canvas {
    // width: 100%;
    // height: 100%;
    position: absolute;
    z-index: -1;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
  }
}
</style>
