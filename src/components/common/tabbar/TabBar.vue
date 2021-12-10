<template>
  <div id="tab-bar">
    <slot></slot>
    <!-- <div class="item">分类</div>
      <div class="item">购物车</div>
      <div class="item">我的</div> -->
  </div>
</template>

<script>
export default {
  name: "TabBar",
};
</script>

<style scoped>
  #tab-bar {
    display: flex;
    position: fixed;
    justify-content: space-between;
    bottom: 0;
    left: 0;
    right: 0;
    background-color: #f6f6f6;
    box-shadow: 0px -2px 1px rgba(100, 100, 100, 0.2);
    
  }
</style> 