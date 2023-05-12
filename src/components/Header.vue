<script setup>
import LeftImg from "../assets/PNG/other/play.png"
import CenterImg from "../assets/PNG/other/center.png"
import RightImg from "../assets/PNG/other/right.png"

</script>

<template>
  <div class="header">
    <div class="left">
      <img :src="LeftImg" alt="" srcset="">
    </div>
    <div class="center">
      <img :src="CenterImg" alt="" srcset="">
    </div>
    <div class="right">
      <img :src="RightImg" alt="" srcset="">
    </div>
  </div>
</template>

<style scoped lang="less">
.header {
  width: 100%;
  height: 60px;
  display: flex;
  align-items: center;
  border-bottom: 2px solid#1211ff;

  .left,
  .center,
  .right {
    display: flex;
    align-items: center;
    height: 60px;

    img {
      width: auto;
      height: 25px;
      object-fit: cover;
      line-height: 60px;
    }
  }
  .left{
    width: 34%;
    border-right: 2px solid#1211ff;
    padding-left: 40px;
    
  }
  .center{
    width: 50%;
    border-right: 2px solid#1211ff;
    padding-left: 20px;
  }

  .right{
    margin:  0 auto;
  }

}
</style>
