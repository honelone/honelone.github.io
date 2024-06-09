<template>
  <div class="card-container">
    <div class="grid" ref="radioGridRef"></div>
  </div>
</template>

<script lang="tsx" setup>
import { onMounted, reactive, ref } from 'vue'

const radioGridRef = ref()

const GRID_SIZE = 18
const RIPPLE_FRAME_TIME = 50
const DEMO_TIMEOUT = 1000 * 5
const rowCount = Math.ceil(window.innerHeight / GRID_SIZE)
const columnCount = Math.ceil(window.innerWidth / GRID_SIZE)

const cells = reactive<any>({})

const isChanging = ref(false)
const demoTiTimer = ref()
const demoInvTimer = ref()

function getDistance(x1, y1, x2, y2) {
  const a = x1 - x2
  const b = y1 - y2
  return Math.sqrt(a * a + b * b)
}

function getRndColor() {
  return '#' + ('000000' + ((Math.random() * 0xffffff) << 0).toString(16)).slice(-6)
}

function getRndInt(min, max) {
  return Math.floor(Math.random() * (max - min + 1)) + min
}

function createGrid() {
  for (let y = 0; y < rowCount; y++) {
    const row = document.createElement('div')
    row.classList.add('grid-row')
    for (let x = 0; x < columnCount; x++) {
      const cell = document.createElement('div')
      cell.classList.add('grid-cell')
      cell.dataset.x = x.toString()
      cell.dataset.y = y.toString()
      row.appendChild(cell)
      cells['x' + x + 'y' + y] = cell
    }
    radioGridRef.value.appendChild(row)
  }
}

function clearOnStates() {
  for (const k in cells) {
    cells[k].classList.remove('on')
  }
}

function drawCircle(px, py, r, color) {
  if (color === undefined) color = 'transparent'

  for (let y = py - r; y <= py + r; y++) {
    if (y < 0 || y >= rowCount) continue
    for (let x = px - r; x <= px + r; x++) {
      if (x < 0 || x >= columnCount) continue

      const d = getDistance(px, py, x, y)
      if (d < r - 1 || d > r) continue

      cells['x' + x + 'y' + y].classList.add('on')
      cells['x' + x + 'y' + y].style.backgroundColor = color
    }
  }
}

function drawCircleDelay(px, py, r, color, timeout) {
  setTimeout(function () {
    drawCircle(px, py, r, color)
  }, timeout || 1)
}

function drawRipple(px, py, color) {
  if (isChanging.value) return false

  isChanging.value = true
  for (let r = 0; r < Math.max(columnCount, rowCount) * 1.5; r++) {
    drawCircleDelay(px, py, r, color, RIPPLE_FRAME_TIME * r)
  }
  setTimeout(function () {
    isChanging.value = false
  }, RIPPLE_FRAME_TIME * (Math.max(columnCount, rowCount) * 1.5))
}

function drawRippleFromEvent(e) {
  if (isChanging.value) return false

  const el = e.target || e.srcElement
  const gx = el.dataset.x
  const gy = el.dataset.y

  clearOnStates()
  drawRipple(gx, gy, getRndColor())
  _waitForDemo()
}

function bindEvents() {
  for (const k in cells) {
    cells[k].addEventListener('click', drawRippleFromEvent, false)
  }
}

function _doRandomRipple() {
  const rx = getRndInt(0, columnCount - 1)
  const ry = getRndInt(0, rowCount - 1)
  clearOnStates()
  drawRipple(rx, ry, getRndColor())
}

function _waitForDemo() {
  clearTimeout(demoTiTimer.value)
  clearInterval(demoInvTimer.value)
  demoTiTimer.value = setTimeout(function () {
    demoInvTimer.value = setInterval(
      _doRandomRipple,
      RIPPLE_FRAME_TIME * (Math.min(rowCount, columnCount) * 2),
    )
  }, DEMO_TIMEOUT)
}

onMounted(() => {
  createGrid()
  bindEvents()
  _waitForDemo()
})
</script>

<style scoped lang="less">
.card-container {
  width: 100%;
  height: 100%;
  background: #222;
  color: white;
  text-align: center;
  :deep(.grid) {
    margin: 0 auto;
    display: inline-block;
    white-space: nowrap;
    .grid-row {
      font-size: 0;
      .grid-cell {
        width: 14px;
        height: 14px;
        display: inline-block;
        margin: 3px;
        cursor: pointer;
        transition: background-color 0.3s linear;
        background-color: #333;
        will-change: background, background-color, transform;

        &:hover {
          background-color: #77ccff !important;
        }

        &.on {
          //background-color: rgba(100, 200, 255, 0.7);
          animation: pop 1s ease-in-out;
          animation-iteration-count: 1;
          @keyframes pop {
            0% {
              transform: scale(1);
            }
            30% {
              transform: scale(1.2);
            }
            60% {
              transform: scale(0.8);
            }
            100% {
              transform: scale(1);
            }
          }
        }
      }
    }
  }
}
</style>
