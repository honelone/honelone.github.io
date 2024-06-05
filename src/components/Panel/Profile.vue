<template>
  <div class="profile custom-card">
    <div class="profile-img">
      <img src="@/assets/avatar.png" />
    </div>
    <div class="profile-text">Hello, Welcome to my page</div>
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
    width: 100%;
    height: 3rem;
    img {
      position: absolute;
      top: -7.2rem;
      width: 10rem;
      border-radius: 50%;
      animation: floatAnimation 2s infinite alternate linear;
    }
  }
  .profile-text {
    font-size: 2rem;
    font-weight: bold;
  }
}
</style>
