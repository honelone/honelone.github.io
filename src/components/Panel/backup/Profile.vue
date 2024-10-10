<template>
  <div class="profile">
    <div class="profile-img">
      <div class="profile-img-inner">
        <img src="@/assets/avatar.png" draggable="false" />
      </div>
    </div>
    <div class="profile-text colorful">Composition</div>
  </div>
</template>

<script setup></script>

<style scoped lang="less">
.profile {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  gap: 12px;
  .profile-img {
    position: relative;
    display: flex;
    justify-content: center;
    width: 8rem;
    height: 8rem;
    border: 4px solid #f6ede4;
    border-radius: 50%;
    .profile-img-inner {
      position: absolute;
      bottom: 0;
      width: 100%;
      height: 100%;
      border-radius: 50%;
      overflow: hidden;
      transition: all 0.5s;
      &:hover {
        bottom: -1px;
        height: 110%;
        border-radius: 0 0 50% 50%;
        img {
          transform: scale(1.2);
        }
      }
      img {
        width: 100%;
        // height: 100%;
        transition: all 0.5s;
        -webkit-user-drag: none;
      }
    }
  }
  .profile-text {
    font-size: 1.3em;
    font-weight: bold;
    pointer-events: none;
    filter: opacity(0.7);
    text-shadow: 1px 1px 1px #000, -1px -1px 1px #fff;

    &.colorful {
      text-shadow: none;
      background: -webkit-linear-gradient(315deg, #f5576c 10%, #fee140 50%, #68e8d8 90%);
      background-clip: text;
      -webkit-background-clip: text;
      -webkit-text-fill-color: transparent;
      background-size: 400% 400%;
      animation: gradientAnimation 20s -10s ease infinite;
    }
  }
}
</style>
