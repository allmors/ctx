<script setup>
import Header from './components/Header.vue'
import Footer from './components/Footer.vue'
import Content from './pages/content/content.vue'

import { onMounted } from "vue"

let isWeixin = ref(false);

onMounted(() => {
  const ua = navigator.userAgent.toLowerCase();
  isWeixin.value = ua.indexOf("micromessenger") !== -1;
})

</script>

<template>
  <div v-if="!isWeixin">
    <Header />
    <Content />
    <Footer />
  </div>
  <div v-else>
    检测到在微信内部打开，请复制链接用浏览器打开！
  </div>
</template>

<style scoped></style>
