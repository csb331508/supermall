<template>
  <div>
    <Swiper>
      <swiper-item v-for="banner in banners">
        <a :href="banner.link">
          <img :src="banner.image" alt="" @load="imgageLoad">
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
  data(){
    return {
      isLoad:false
    }
  },
  components:{
    Swiper,
    SwiperItem
  },
  methods:{

    imgageLoad(){
      if(!this.isLoad){
        this.$emit('swiperImageLoad')
        this.isLoad = true
      }
      
    }
    // swiperImageLoad
  }
}
</script>

<style scoped>

</style>