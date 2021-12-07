<template>
  <div>
    <nav-bar class="home-nav">
      <div slot="center">购物街</div>
    </nav-bar>
    <home-swiper :banners="banners"> </home-swiper>
    <recommend-view :recommends="recommends"></recommend-view>

    

  </div>
</template>

<script>
import NavBar from "components/common/navbar/NavBar";
import HomeSwiper from "./childComps/HomeSwiper.vue";
import RecommendView from './childComps/RecommendView.vue'
import { getHomeMultidata } from "network/home";

export default {
  name: "Home",
  components: {
    NavBar,
    HomeSwiper,
    RecommendView
  },
  data() {
    return {
      banners: [],
      recommends: [],
    };
  },
  created() {
    getHomeMultidata()
      .then((res) => {
        this.banners = res.data.banner.list;
        // console.log(res.data.banner.list);
        

        // console.log(this.banners);
        this.recommends = res.data.recommend.list;
        console.log(this.recommends);
      })
      .catch((err) => {
        console.log(err);
      });
  },
};
</script>

<style>
.home-nav {
  background-color: var(--color-tint);
  color: white;
}
</style>