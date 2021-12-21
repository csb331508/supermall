<template>
  <div id="#home">
    <nav-bar class="home-nav">
      <div slot="center">购物街</div>
    </nav-bar>
    <tab-control
        :titles="['流行', '新款', '精选']"
        ref="tabControl1"
        @tabclick="tabclick"
        v-show="true"
        class="tabcontrol"
      >
    </tab-control>
    <scroll
      class="wrapper"
      ref="scroll"
      :probe-type="3"
      :pull-up-load="true"
      @scroll="contentScroll"
      @pullingUp ="loadMore"
    >
      <home-swiper :banners="banners" class="home-swiper" @swiperImageLoad ="swiperImageLoad"> </home-swiper>
      <recommend-view :recommends="recommends"></recommend-view>
      <feature-view></feature-view>
      <tab-control
        :titles="['流行', '新款', '精选']"
        ref="tabControl2"
        @tabclick="tabclick"
      ></tab-control>
      <goods-list :goods="showGoods"></goods-list>
    </scroll>
    <back-top @click.native="backClick" v-show="isBackshow"></back-top>
  </div>
</template>

<script>
import NavBar from "components/common/navbar/NavBar";
import scroll from "components/common/scroll/Scroll.vue";
import TabControl from "components/content//tabControl/TabControl";
import BackTop from "components/content/backTop/BackTop.vue";
import HomeSwiper from "./childComps/HomeSwiper.vue";
import GoodsList from "components/content/goods/GoodsList.vue";
import RecommendView from "./childComps/RecommendView.vue";
import FeatureView from "./childComps/FeatureView.vue";
import { getHomeMultidata, getHomeGoods } from "network/home";
import Scroll from "../../components/common/scroll/Scroll.vue";
import {debounce} from 'common/utils.js'
export default {
  name: "Home",
  components: {
    NavBar,
    scroll,
    BackTop,
    TabControl,
    HomeSwiper,
    GoodsList,
    RecommendView,
    FeatureView,
  },
  computed: {
    showGoods() {
      return this.goods[this.currentType].list;
    },
  },
  data() {
    return {
      banners: [],
      recommends: [],
      goods: {
        pop: { page: 0, list: [] },
        new: { page: 0, list: [] },
        sell: { page: 0, list: [] },
      },
      currentType: "pop",
      isBackshow: false,
      isFixed:false,
      tabControlOffsetTop:0
    };
  },
  created() {
    this.getHomeMultidata(); //请求导航条数据
    this.getHomeGoods("pop");
    this.getHomeGoods("new");
    this.getHomeGoods("sell");
  },
  mounted() {
    const refresh = debounce(this.$refs.scroll.refresh,200)
    this.$bus.$on("itemImgLoad", () => {
      
      refresh()
    
    });
  },
  destoryed(){
    console.log(destoryed);
  },
  methods: {
      
   
    // 事件监听相关
    tabclick(index) {
      // console.log(index);
      switch (index) {
        case 0:
          this.currentType = "pop";

          break;
        case 1:
          this.currentType = "new";

          break;
        case 2:
          this.currentType = "sell";

          break;
      }
      this.$refs.TabControl.currentIndex = index;
      this.$refs.TabContro2.currentIndex = index;
    },
    swiperImageLoad(){
      // console.log(this.$refs.tabControl.$el.offsetTop);
      this.tabControlOffsetTop = this.$refs.tabControl2.$el.offsetTop
      console.log(this.tabControlOffsetTop );
      
    },
    // 下拉加载更多
    loadMore(){
      console.log('more');
      this.getHomeGoods(this.currentType);
    },
    // 回到顶部
    backClick() {
      // console.log(this.$refs.scroll.test);
      // this.$refs.scroll.scrollTo(0,0)
      this.$refs.scroll.scrollTo(0, 0, 900);
    },
    // 显示隐藏顶部按钮
    contentScroll(position) {
      console.log(this.$refs.scroll.scroll.y);
      // this.isBackshow = (-position.y )> 1000;
      // // this.tabControlOffsetTop = this.$refs.tabControl.$el.offsetTop
      // if((-position.y )<this.tabControlOffsetTop){
      //   console.log('111');
      //   isFixed = true
      
      // console.log(this.$$refs.scroll.test);
    },

    // 网络请求相关
    getHomeMultidata() {
      getHomeMultidata()
        .then((res) => {
          this.banners = res.data.banner.list;
          // console.log(res.data.banner.list);

          // console.log(this.banners);
          this.recommends = res.data.recommend.list;
          // console.log(this.recommends);
        })
        .catch((err) => {
          console.log(err);
        });
    },
    getHomeGoods(type) {
      const page = this.goods[type].page + 1;
      getHomeGoods(type, page).then((res) => {
        // console.log(res.data.list);
        // console.log(res.data[type].list);
        this.goods[type].list.push(...res.data.list);
        this.goods[type].page +=1;
        this.$refs.scroll.finishPullUp();
      });
    },
  },
};
</script>

<style scoped>
#home {
  position: relative;
  height: 100vh;
}
.wrapper {
  position: absolute;
  height: 100vh;
  top: 44px;
  bottom: 49px;
  left: 0;
  right: 0;
  /* height: calc(100% -93px);
  overflow: hidden;
  margin-top: 44px; */
}
.home-nav {
  background-color: var(--color-tint);
  color: white;
  position:fixed;
  left: 0;
  top: 0;
  right: 0;
  z-index: 1;
}

.tab-control {
  /* position: sticky; */
  top: 44px;
}
.tabcontrol{
  /* display: flex; */
  width: 100%;
  position:fixed;
  top: 44px;
  z-index: 9;
}
</style>