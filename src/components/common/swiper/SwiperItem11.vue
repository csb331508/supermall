<template>
  <div>
    <div class="swiper-item"><slot></slot></div>
  </div>
</template>

<script>
export default {
  name:'SwiperItem'
}
</script>

<style>
.swiper-item{
  width: 375px;
  /* position: absolute; */
  left: 0;
  top: 0;
}
.swiper-item img{
  /* width: 100%; */
  width: 100%;
  
}
</style>