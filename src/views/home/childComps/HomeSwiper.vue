<template>
  <div>
    <Swiper>
      <swiper-item v-for="banner in banners">
        <a :href="banner.link">
          <img :src="banner.image" alt="">
        </a>
      </swiper-item>
    </Swiper>
  </div>
</template>

<script>
import {Swiper,SwiperItem} from 'components/common/swiper'

export default {
  name:'HomeSwiper',
  props:{
    banners:{
      type:Array,
      default:[]
    }
  },
  components:{
    Swiper,
    SwiperItem
  }
}
</script>

<style scoped>

</style>