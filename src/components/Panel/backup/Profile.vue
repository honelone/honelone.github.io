<template>
  <div class="profile custom-card">
    <div class="profile-img">
      <div class="profile-img-inner">
        <img src="@/assets/avatar.png" />
      </div>
    </div>
    <div class="profile-back">Composition</div>
  </div>
</template>

<script setup></script>

<style scoped lang="less">
.profile {
  .profile-img {
    position: relative;
    display: flex;
    justify-content: center;
    width: 12.5rem;
    height: 12.5rem;
    border: 4px solid #f6ede4;
    border-radius: 50%;
    .profile-img-inner {
      position: absolute;
      bottom: 0;
      width: 100%;
      height: 100%;
      border-radius: 50%;
      overflow: hidden;
      transition: all 0.3s;
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
        transition: all 0.3s;
      }
    }
  }
  .profile-back {
    font-size: 2em;
    font-weight: bold;
    pointer-events: none;
    filter: opacity(0.7);
    background: linear-gradient(45deg, #f5576c 10%, #fee140 100%);
    background-clip: text;
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
    // background-size: 200% 200%;
  }
}
</style>
