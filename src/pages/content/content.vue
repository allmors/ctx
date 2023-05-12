<script setup>
import { ref, reactive, watch, onMounted } from "vue";
import Modal from "../../components/modal/index.vue"
// top
import TIP from "../../assets/PNG/other/TIP.png"
import A from "../../assets/PNG/header/A.png"
import B from "../../assets/PNG/header/B.png"
import C from "../../assets/PNG/header/C.png"
import D from "../../assets/PNG/header/D.png"
import E from "../../assets/PNG/header/E.png"
import F from "../../assets/PNG/header/F.png"
import G from "../../assets/PNG/header/G.png"
import H from "../../assets/PNG/header/H.png"
import I from "../../assets/PNG/header/I.png"
import J from "../../assets/PNG/header/J.png"
// aside
import a from "../../assets/PNG/aside/1.png"
import b from "../../assets/PNG/aside/2.png"
import c from "../../assets/PNG/aside/3.png"
import d from "../../assets/PNG/aside/4.png"
import e from "../../assets/PNG/aside/5.png"

const topList = reactive([
  { url: TIP, id: "TIP" },
  { url: A, id: "A" },
  { url: B, id: "B" },
  { url: C, id: "C" },
  { url: D, id: "D" },
  { url: E, id: "E" },
  { url: F, id: "F" },
  { url: G, id: "G" },
  { url: H, id: "H" },
  { url: I, id: "I" },
  { url: J, id: "J" }
])

const asideList = reactive([
  { url: a, id: "1" },
  { url: b, id: "2" },
  { url: c, id: "3" },
  { url: d, id: "4" },
  { url: e, id: "5" },
])


let imgSrc = ref(null);
let imgName = ref(null);
let src = ref(null);
let topIndex = ref(-1);
let asideIndex = ref(-1);
let audioSrc = ref(null);
let autoplay = ref(false);
let visible = ref(false);
let isWeixin = ref(false);

watch([imgName, imgSrc], () => {
  if (imgName.value && imgSrc.value) {
    src.value = new URL(`../../assets/GIF/${imgSrc.value}/${imgSrc.value}${imgName.value}.gif`, import.meta.url).href
    audioSrc.value = new URL(`../../assets/music/${imgSrc.value}.mp3`, import.meta.url).href;
  }
}, {
  immediate: true
})

const handleClickAside = (item, index) => {
  asideIndex.value = index;
  imgName.value = item.id;
}

const handleClickTop = (item, index) => {
  if (index === 0) return
  if (imgName.value == null || '') {
    visible.value = true
    return;
  }
  topIndex.value = index;
  imgSrc.value = item.id;
  autoplay.value = true;
}

const handleClear = () => {
  imgName.value = null;
  imgSrc.value = null;
  topIndex.value = -1;
  asideIndex.value = -1;
}

const confirm = () => {
  visible.value = false
}
const update = () => {
  visible.value = false
}

onMounted(() => {
  const ua = navigator.userAgent.toLowerCase();
  isWeixin.value = ua.indexOf("micromessenger") !== -1;
})


</script>

<template>
  <div class="content" v-if="!isWeixin">
    <div class="top">
      <div class="top_img " v-for="(item, index) in topList" :key="item.id" @click="handleClickTop(item, index)">
        <img :src="item.url" alt="" srcset="">
        <div class="top_active" v-if="topIndex == index"></div>
      </div>
    </div>
    <div class="ac">
      <div class="aside">
        <div class="aside_img" v-for="(item, index) in asideList" :key="item.id" @click="handleClickAside(item, index)">
          <img :src="item.url" alt="" srcset="">
          <div class="aside_active" v-if="asideIndex == index"></div>
        </div>
      </div>
      <div class="center" @click="handleClear" v-if="imgName && imgSrc">
        <img :src=src alt="" srcset="" @click.stop>
        <audio :src="audioSrc" :autoplay="autoplay" loop="loop" @click.stop>
          Your browser does not support the audio element.
        </audio>
      </div>
    </div>
    <Modal title="温馨提示:)" @confirm="confirm" @update="update" :visible="visible">您需要先选择左侧再点击该区域！</Modal>
  </div>
  <div v-else>
    检测到在微信内部打开，请复制链接用浏览器打开！
  </div>
</template>

<style scoped lang="less">
.content {
  width: 100%;
  height: 100%;
  padding: 15px 40px;
  margin-bottom: 10px;
  background-color: #fbfbfb;
  user-select: none;

  .top {
    display: flex;
    align-items: center;
    justify-content: space-between;
    width: 100%;
    margin-bottom: 10px;

    .top_img {
      width: 6rem;
      height: 6rem;
      cursor: pointer;
      position: relative;

      img {
        width: 100%;
        height: 100%;
        -webkit-user-drag: none;
      }
    }

    .top_active {
      position: absolute;
      left: 0;
      width: 6rem;
      border-bottom: .6rem solid #00efff;
    }
  }

  .ac {
    display: flex;
    width: 100%;
    height: 100%;

    .aside {
      display: flex;
      align-items: center;
      justify-content: start;
      flex-wrap: wrap;
      width: 120px;
      height: 650px;

      .aside_img {
        width: 6rem;
        height: 6rem;
        margin: 15px 0;
        cursor: pointer;
        position: relative;

        img {
          width: 100%;
          height: 100%;
          -webkit-user-drag: none;
        }
      }

      .aside_active {
        position: absolute;
        top: 0;
        right: -20px;
        height: 6rem;
        margin-left: 16px;
        border-right: .6rem solid #00efff;
      }
    }

    .center {
      width: 100%;
      height: 650px;
      display: flex;
      justify-content: center;

      img {
        width: 40%;
        height: 100%;
        object-fit: cover;
        -webkit-user-drag: none;
      }
    }
  }

}
</style>
