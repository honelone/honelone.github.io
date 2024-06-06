<template>
  <div class="profile custom-card">
    <div class="profile-img">
      <div class="profile-img-inner">
        <img src="@/assets/avatar.png" />
      </div>
    </div>
    <div class="profile-text">Hello, Welcome to my page</div>
    <div class="profile-back">Composition</div>
  </div>
</template>

<script setup></script>

<style scoped lang="less">
.profile {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  .profile-img {
    position: relative;
    display: flex;
    justify-content: center;
    width: 10rem;
    height: 10rem;
    border: 4px solid #f6ede4;
    border-radius: 50%;
    .profile-img-inner {
      position: absolute;
      bottom: 0;
      width: 10rem;
      height: 10rem;
      border-radius: 50%;
      overflow: hidden;
      transition: all 0.3s;
      &:hover {
        bottom: -1px;
        height: 11rem;
        border-radius: 0 0 50% 50%;
        img {
          transform: scale(1.2);
        }
      }
      img {
        width: 10rem;
        height: 10rem;
        transition: all 0.3s;
      }
    }
  }
  .profile-text {
    font-size: 2rem;
    font-weight: bold;
  }
  .profile-back {
    position: absolute;
    top: 50%;
    left: 50%;
    z-index: -1;
    transform: translate(-50%, -50%);
    font-size: 4em;
    font-weight: bold;
    pointer-events: none;
    filter: opacity(0.3);
    background: linear-gradient(45deg, #52e5e7 10%, #130cb7 100%);
    background-clip: text;
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
  }
}
</style>
