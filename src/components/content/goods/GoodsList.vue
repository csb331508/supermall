<template>
  <div class="goods">
    <div v-for="item in goods">
      <goods-list-item :item="item" class="item"></goods-list-item>
    </div>
  </div>
</template>

<script>
import GoodsListItem from './GoodsListItem.vue';
export default {
  name:'GoodsList',
  props:{
    goods:{
      type:Array,
      default(){
        return []
      }
    }
  },

  components:{
    GoodsListItem
  }
}
</script>

<style scoped>
  .goods{
    display: flex;
    width: 100vm;
    margin: 0 auto;
    justify-content: space-around;
    flex-wrap: wrap;
    margin-bottom: 53px;
  }

</style>