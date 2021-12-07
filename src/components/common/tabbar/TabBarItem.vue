<template>
  <div class="tab-bar-item" @click="itemClick">
    <!-- <div>首页</div>
    <img src="../../assets/img/tabbar/home.svg" alt=""> -->

    <div v-if="!isActive">
      <slot name="item-icon"></slot>
    </div>

    <div class="item-icon-active" v-else>
      <slot name="item-icon-active"></slot>
    </div>

    <div :style="activeStyle">
      <slot name="item-text"></slot>
    </div>
  </div>
</template>

<script>
export default {
  name: "TabBarItem",
  data() {
    return {
      name:''
    };
  },
  props:{
    path:String,
    activeColor:{
      type:String,
      default:'red'
    }
  },
  computed:{
    isActive(){
      return this.$route.path.indexOf(this.path) !== -1;
    },
    activeStyle(){
      return this.isActive ? {color:this.activeColor} : {}
    },
  },
  methods:{
    itemClick(){
      this.$router.replace(this.path).catch(err => err)
      
    }
  }
};
</script>

<style>
.tab-bar-item {
  flex: 1;
  height: 49px;
  text-align: center;
  font-size: 14px;
}

.tab-bar-item img {
  width: 24px;
  height: 24px;
  margin-top: 3px;
  margin-bottom: -3px;
}
</style>