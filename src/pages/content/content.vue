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
    // src.value = `src/assets/GIF/${imgSrc.value}/${imgSrc.value}${imgName.value}.gif`;
    // audioSrc.value = `src/assets/music/${imgSrc.value}.mp3`;

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
    <div class="center" v-if="imgName && imgSrc">
      <img :src=src alt="" srcset="">
      <div class="clear" @click="handleClear">清除数据</div>
      <audio :src="audioSrc" :autoplay="autoplay">
        Your browser does not support the audio element.
      </audio>
    </div>
    <div class="aside">
      <div class="aside_img" v-for="(item, index) in asideList" :key="item.id" @click="handleClickAside(item, index)">
        <img :src="item.url" alt="" srcset="">
        <div class="aside_active" v-if="asideIndex == index"></div>
      </div>
    </div>
    <Modal title="温馨提示😊" @confirm="confirm" @update="update" :visible="visible">您需要先选择左侧再点击该区域！</Modal>
  </div>
  <div v-else>
    检测到在微信内部打开，请复制链接用浏览器打开！
  </div>
</template>

<style scoped lang="less">
.content {
  width: 100%;
  height: 100%;
  padding: 15px 10px 15px 60px;
  border-bottom: 2px solid blue;
  border-top: 2px solid blue;
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
      margin-top: 8px;
      border-bottom: .6rem solid #00efff;
    }
  }

  .aside {
    display: flex;
    align-items: center;
    justify-content: space-between;
    flex-wrap: wrap;
    width: 120px;

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
    position: absolute;
    left: 50%;
    top: 50%;
    transform: translate(-50%, -50%);
    width: 30%;
    height: 40%;

    img {
      width: 100%;
      height: 100%;
      object-fit: contain;
      -webkit-user-drag: none;

    }

    .clear {
      text-align: center;
      width: 100%;
      height: 40px;
      line-height: 40px;
      border-radius: 50px;
      color: #725bda;
      font-size: 1rem;
      font-weight: bolder;
      letter-spacing: 2px;
      box-shadow: 0 0 10px #eeeeee;
      cursor: pointer;
    }

    .clear::after {
      content: '';
      background: inherit;
      filter: blur(10px);
    }
  }
}
</style>
