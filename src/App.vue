<script setup lang='ts'>
import CompareImage from './views/CompareImage.vue';
import {ImgComparisonSlider} from '@img-comparison-slider/vue';
import imageLeft from '@/assets/img/common/img1.jpg';
import imageRight from '@/assets/img/common/img2.jpg';
import {NButton} from 'naive-ui'

import {ref} from 'vue';

const scale = ref('1:1')

function changeScale(scaleText: string) {
  scale.value = scaleText
  console.log(scaleText)
}

</script>

<template>
  <div class="flow">
    <button @click="changeScale('1:1')">1:1</button>
    <button @click="changeScale('1:2')">1:2</button>
    <button @click="changeScale('3:4')">3:4</button>
    <button @click="changeScale('9:16')">9:16</button>
    <button @click="changeScale('16:9')">16:9</button>
    <button @click="changeScale('4:3')">4:3</button>
    <NButton type="primary">测试按钮</NButton>
  </div>
  <div class="wrapper">
    <!--      图片对比的效果-->
    <CompareImage scale="1:1" height='300'/>
    <CompareImage scale="1:2" height='300'/>
    <CompareImage scale="3:4" height='300'/>
    <CompareImage scale="9:16" height='300'/>
    <!--      图片对比的效果-->
    <ImgComparisonSlider tabindex="0" class="rendered">
      <figure slot="first" class="before">
        <img style="width: 100%" src="https://img-comparison-slider.sneas.io/demo/images/before.webp">
        <figcaption>Before</figcaption>
      </figure>
      <figure slot="second" class="after">
        <img style="width: 100%" src="https://img-comparison-slider.sneas.io/demo/images/after.webp">
        <figcaption>After</figcaption>
      </figure>
    </ImgComparisonSlider>
    <img :src="imageLeft">
    <img :src="imageRight">
  </div>
</template>

<style scoped>
header {
  line-height: 1.5;
}

.before,
.after {
  margin: 0;
}

.before figcaption,
.after figcaption {
  background: #fff;
  border: 1px solid #c0c0c0;
  border-radius: 12px;
  color: #2e3452;
  opacity: 0.8;
  padding: 12px;
  position: absolute;
  top: 50%;
  transform: translateY(-50%);
  line-height: 100%;
}

.before figcaption {
  left: 12px;
}

.after figcaption {
  right: 12px;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }
}
</style>
