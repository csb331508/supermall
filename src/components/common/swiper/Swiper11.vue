<template>
  <div id="slide-outer">
    <div class="swiper">
      <slot></slot>
      <button @click="handelDom">test</button>
    </div>
  </div>
</template>

<script>
export default {
  name: "Swiper",
  props: {
    slideTime: {
      type: Number,
      default: 5000,
    },
  },
  data() {
    return {
      slideWidth: 0, //单个图片宽度
      totalWidth: 0, //图片总长度
      sliderCount: 0, //图片个数
      index:0,
      currentIndex:0
    };
  },

  methods: {
    

    startTimer() {
      
    },
    // 处理dom元素
    handelDom() {
      let slideOuter = document.querySelector("#slide-outer");
      let swiper = document.querySelector(".swiper");
      this.slideWidth = slideOuter.offsetWidth; //单个图片宽度
      this.totalWidth = swiper.offsetWidth; //所有图片宽度
      this.sliderCount = this.totalWidth / this.slideWidth;//所有图片个数
      console.log(this.sliderCount);
    },
  },
};
</script>

<style scoped>
#slide-outer {
  position: relative;
}
.swiper {
  /* width: 375px; */
  display: flex;

  /* overflow: hidden; */
}
</style>