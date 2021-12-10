<template>
  <div class="wrapper" ref="wrapper">
    <div class="content">
      <slot></slot>
    </div>
  </div>
</template>

<script>
import BScroll from "better-scroll";
export default {
  name: "Scroll",
  data() {
    return {
      scroll: null,
      pos: 0,
      test: "111",
    };
  },
  props: {
    probeType: {
      type: Number,
      default: 0,
    },
    pullUpLoad: {
      type: Boolean,
      default: false,
    },
  },
  created() {},
  mounted() {},

  updated() {
    // 创建bscroll对象
    this.scroll = new BScroll(this.$refs.wrapper, {
      click: true,
      probeType: this.probeType,
      pullUpLoad: this.pullUpLoad,
      // mouseWheel: true,
    });
    // 监听滚动的位置
    this.scroll.on("scroll", (position) => {
      //  console.log(position);
      this.$emit("scroll", position);
    });
    console.log(this.scroll);

    // 上拉加载更多
    this.scroll.on("pullingUp", () => {
      this.$emit("pullingUp");
    });
  },
  methods: {
    // 封装scrollTo函数
    scrollTo(x, y, time = 300) {
      // console.log(this.scroll);
      console.log('111');
      this.scroll.scrollTo(x, y, time);
      // console.log(this.scroll.scrollTo);
      // this.scroll(scrollTo(x, y, time));
      // this.$refs.scroll.scroll.refresh()
    },
    // 封装finishpullup函数
    finishPullUp(){
      this.scroll.finishPullUp()
    },
    refresh(){
      this.scroll.refresh()
    }
  },
};
</script>

<style scoped>
</style>