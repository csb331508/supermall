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

    // console.log(this.scroll);
    // if (this.probeType === 2 || this.probeType === 3) {
      // 监听滚动的位置
      this.scroll.on("scroll", (position) => {
        //  console.log(position);
        this.$emit("scroll", position);
      });
    // }
    // 下拉加载更多
    if (this.pullUpLoad) {
      this.scroll.on("pullingUp", () => {
        this.$emit("pullingUp");
        console.log("监听滚动到底部");
      });
    }
  },
  methods: {
    // 封装scrollTo函数
    scrollTo(x, y, time = 300) {
      console.log("111");
      this.scrollTo && this.scroll.scrollTo(x, y, time);
    },

    // 封装finishpullup函数
    finishPullUp() {
      this.scroll && this.scroll.finishPullUp();
    },

    refresh() {
      this.scroll && this.scroll.scrollTo && this.scroll.refresh();
      console.log("----------");
    },
  },
};
</script>

<style scoped>
</style>