<script setup>
import LeftImg from "../assets/PNG/other/buttom_left.png";
import smile from "../assets/PNG/other/smile.png";
</script>

<template>
  <div class="footer">
    <div class="left">
      <img :src="LeftImg" alt="" srcset="">
    </div>
    <div class="right">
      <img :src="smile" alt="" srcset="">
    </div>
  </div>
</template>

<style scoped lang="less">
.footer {
  width: 100%;
  height: 60px;
  display: flex;
  justify-content: space-between;
  align-items: center;
  border-top: 2px solid #1211ff;
  padding: 0 40px;

  .left,
  .right {
    display: flex;
    align-items: center;
    height: 60px;
  }

  .left {
    img {
      width: auto;
      height: 25px;
      object-fit: cover;
    }
  }

  .right {
    width: 40px;
    height: 40px;

    img {
      width: 100%;
      height: 100%;
      object-fit: cover;
    }
  }
}
</style>
