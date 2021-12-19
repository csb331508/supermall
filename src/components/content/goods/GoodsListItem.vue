<template>
  <div>
    <div class="item">
      <a :href="item.link">
        <img :src="item.show.img" alt="" @load="imgLoad"/>

        <div class="goodsMessage">
          <span>{{ item.title }}</span>
          <div class="itemcenter">
            <span class="price">￥{{ item.price }}</span>
            <span class="cfav">✩{{ item.cfav }}</span>
          </div>
        </div>
      </a>
    </div>
  </div>
</template>

<script>
export default {
  name: "GoodsListItem",
  props: {
    item: {
      type: Object,
      default() {
        return {};
      },
    },
  },
  methods:{
    imgLoad(){
      // console.log('--------');
      this.$bus.$emit('itemImgLoad')
    }
  }
};
</script>

<style scoped>
.item {
  width: 170px;
}
.item a{
  width: 100%
}

.item img {
  width: 100%;
  border-radius: 10px;
}
.goodsMessage {
  width: 100%;
}
.item span {
  font-size: 12px;
  display: inline-block;
  width: 100%;
  overflow: hidden;
  white-space: nowrap;
  text-overflow: ellipsis;
  -o-text-overflow: ellipsis;
}
.itemcenter {
  display:flex;
  justify-content:flex-start;
  text-align: center;
  /* padding: 0 40px; */
}
.itemcenter span{
  text-align: center;
}
.price {
  color: pink;
}
</style>