<template>
  <div class="main-box" :style="`height: ${height}rem;`">
    <div class="img_drag_change">
      <div ref="imgBox" class="img-box">
        <div ref="beforeImg" class="before-img">
          <div class="info">Before</div>
          <img :src="props.beforeUrl"/>
        </div>
        <div ref="afterImg" class="after-img" :style="`left: ${left}%;`">
          <div :style="`right: ${left}%;`" class="info">After</div>
          <img :style="`left: -${left}%;`" :src="props.afterUrl"/>
        </div>
      </div>
      <!-- 分割线 -->
      <div class="divide_line" ref="divide_line" :style="`left: ${left}%;`">
        <div class="item">
          <!-- 需要增加手机端兼容事件 -->
          <div class="icon-box" @touchstart="mousedown" @mousedown="mousedown"/>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { defineProps, ref, onMounted } from 'vue';
// 引入两张图片
import img_left from '@/assets/img/common/img1.jpg';
import img_right from '@/assets/img/common/img2.jpg';
// 父组件传值
let props = defineProps({
  height: {
    type: Number,
    default: 0,
  },
  beforeUrl: {
    type: String,
    default: img_left,
  },
  afterUrl: {
    type: String,
    default: img_right
  }
})

// imgbox
let imgBox = ref(null); // 盒子
let imgBoxWidth = ref(0); // 盒子宽度
let beforeImg = ref(null); // 第一张图片
let afterImg = ref(null); // 第二张图片
let left = ref(0); // 初始的 left
let rem = ref(0.0625); // px转rem
let height = ref(500); //默认高度
let divide_line = ref('null'); // 分割线节点

if (props.height > 0) {
  height.value = props.height * rem.value;
} else if (props.height == 'auto') {
  height = 'auto';
} else {
  height.value = height.value * rem.value;
}


onMounted(() => {
  imgBoxWidth.value = imgBox.value.offsetWidth;
  left.value = 50;
})

let range = function (num, min, max) {
  if (num < min) {
    return min;
  }
  if (num > max) {
    return max;
  }
  return num;
}

// 需要加兼容手机端事件
// 鼠标按下事件
const mousedown = (e) => {
  // 拿到盒子宽度
  imgBoxWidth.value = imgBox.value.offsetWidth;
  let min = 8 / imgBoxWidth.value * 100;
  let startX = e.clientX || e.touches[0].pageX; // 鼠标按下的初始 clientX 值
  let divideLineLeft = divide_line.value.offsetLeft; //获取盒子的初始left值

  console.log(e, startX, divideLineLeft);
  // 鼠标移动事件
  let onmousemove = (e) => {
    let moveLeft = (e.clientX || (e.touches && e.touches[0].pageX) || 0) - startX; // 拿到鼠标移动的 moveLeft，e.touches[0]是兼容移动端，加上 || 0 是因为在 PC 端鼠标向左移出浏览器时会报错
    let l = (divideLineLeft + moveLeft) / imgBoxWidth.value * 100;
    left.value = range(l, min, 100 - min);
  }
  document.addEventListener('mousemove', onmousemove);
  document.addEventListener('touchmove', onmousemove);

  // 鼠标抬起事件
  let onmouseup = (e) => {
    // 清除移动和抬起事件
    document.removeEventListener('mousemove', onmousemove);
    document.removeEventListener('touchmove', onmousemove);
    document.removeEventListener('mouseup', onmouseup);
    document.removeEventListener('touchend', onmouseup);
  }
  document.addEventListener('mouseup', onmouseup);
  document.addEventListener('touchend', onmouseup);
  return false; //阻止默认事件
}
</script>

<style lang="scss" scoped>

.main-box {
  height: 100%;
}

.img_drag_change {
  user-select: none; // 控制页面文字不能被选中
  margin: 0;
  position: relative;
  top: 12px;
  height: calc(100% - 24px);
}

.img-box {
  font-size: 0;
  width: 100%;
  top: 8px;
  height: calc(100% - 16px);
  overflow: hidden;
  position: relative;
  border-radius: 12px;

  > div.after-img {
    position: absolute;
    left: 0;
    z-index: 1;
  }

  > div {
    position: relative;
    left: 0;
    width: 100%;
    height: 100%;
    top: 0;
    overflow: hidden;
    background-color: #AAAAAA;

    .info {
      position: absolute;
      color: #000000;
      background-color: white;
      z-index: 1;
      opacity: 0.72;
      font-size: 14px;
      white-space: nowrap;
      overflow: hidden;
      height: 22px;
      padding-left: 10px;
      padding-right: 10px;
      align-content: center;
      border-radius: 4px;
      margin: 1rem;
    }

    > img {
      width: 100%;
      height: 100%;
      object-fit: cover;
      position: relative;
      top: 0;
      left: 0;
    }

  }

  > div.after-img .info {
    text-align: right;
    right: 0;
  }
}


.divide_line {
  width: 2px;
  height: 100%;
  top: 0;
  left: 50px;
  background: #dddddd;
  position: absolute;
  z-index: 1;
  overflow: visible;
  pointer-events: none; // pointer-events：是否对指针事件做出反应。none：元素不能对鼠标事件做出反应

  .item {
    height: 100%;
    display: flex;
    align-items: center;
    width: 10px;
    position: relative;
    pointer-events: auto; // auto：默认值，设置该属性链接可以正常点击访问。
  }

  .icon-box {
    position: absolute;
    left: -1rem;
    font-size: 1rem;
    height: 500px;
    width: 30px;
    color: #dddddd;
    display: flex;
    align-items: center;
    justify-content: center;
    margin-left: 1px;
    transition: all .1s;

    span {
      cursor: pointer;
    }
  }

}
</style>
