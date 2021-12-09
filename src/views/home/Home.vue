<template>
  <div>
    <nav-bar class="home-nav">
      <div slot="center">购物街</div>
    </nav-bar>
    <home-swiper :banners="banners" class="home-swiper"> </home-swiper>
    <recommend-view :recommends="recommends"></recommend-view>
    <feature-view></feature-view>
    <tab-control
      :titles="['流行', '新款', '精选']"
      class="tab-control"
      @tabclick="tabclick"
    ></tab-control>
    <goods-list :goods="showGoods"></goods-list>
    <!-- <ul>
      <li>1111111</li>
      <li>1111111</li>
      <li>1111111</li>
      <li>1111111</li>
      <li>111</li>
      <li>111</li>
      <li>111</li>
      <li>111</li>
      <li>111</li>
      <li>111</li>
      <li>111</li>
      <li>111</li>
      <li>111</li>
      <li>111</li>
      <li>111</li>
      <li>111</li>
      <li>111</li>
      <li>111</li>
      <li>111</li>
      <li>111</li>
      <li>111</li>
      <li>111</li>
      <li>111</li>
      <li>111</li>
      <li>111</li>
      <li>111</li>
      <li>111</li>
      <li>111</li>
      <li>111</li>
      <li>111</li>
      <li>111</li>
      <li>111</li>
      <li>111</li>
      <li>111</li>
      <li>111</li>
      <li>111</li>
      <li>111</li>
      <li>111</li>
      <li>111</li>
      <li>111</li>
      <li>111</li>
      <li>111</li>
      <li>111</li>
      <li>111</li>
      <li>111</li>
      <li>111</li>
      <li>111</li>
      <li>111</li>
    </ul> -->
  </div>
</template>

<script>
import NavBar from "components/common/navbar/NavBar";
import TabControl from "components/content//tabControl/TabControl";
import HomeSwiper from "./childComps/HomeSwiper.vue";
import GoodsList from "components/content/goods/GoodsList.vue";
import RecommendView from "./childComps/RecommendView.vue";
import FeatureView from "./childComps/FeatureView.vue";
import { getHomeMultidata, getHomeGoods } from "network/home";

export default {
  name: "Home",
  components: {
    NavBar,
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
    };
  },
  created() {
    this.getHomeMultidata(); //请求导航条数据
    this.getHomeGoods("pop");
    this.getHomeGoods("new");
    this.getHomeGoods("sell");
  },
  methods: {
    // 事件监听相关
    tabclick(index) {
      // console.log(index);
      switch(index){
        case 0:
          this.currentType = 'pop';
          
          break;
        case 1:
          this.currentType ='new';
          
          break;
        case 2:
          this.currentType ='sell';
          
          break;
      }
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
        console.log(res.data.list);
        // console.log(res.data[type].list);
        this.goods[type].list.push(...res.data.list);
        this.goods[type].page = page;
      });
    },
  },
};
</script>

<style>
.home-nav {
  background-color: var(--color-tint);
  color: white;
  position: fixed;
  left: 0;
  top: 0;
  right: 0;
  z-index: 1;
}
.home-swiper {
  padding-top: 44px;
}
.tab-control {
  position: sticky;
  top: 44px;
}
</style>