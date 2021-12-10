<template>
  <div class="TabControl">
    <div
      id="item"
      v-for="(item, index) in titles"
      :class="{ tabcontrolItem: index === currentIndex }"
      @click="itemClick(index)"
    >
      <span>{{ item }}</span>
    </div>
  </div>
</template>

<script>
export default {
  name: "TabControl",
  props: {
    titles: {
      type: Array,
      default() {
        return [];
      },
    },
  },
  data() {
    return {
      currentIndex: 0,
    };
  },
  methods: {
    itemClick(index) {
      this.currentIndex = index;
      this.$emit('tabclick',index)
      
    },
  },
};
</script>

<style scoped>
.TabControl {
  display: flex;
  text-align: center;
  height: 40px;
  line-height: 40px;
  background-color: #fff;
}
#item {
  flex: 1;
}

.tabcontrolItem span {
  color: pink;
  padding: 3px 5px;
  border-bottom: pink 3px solid;
  
}
</style>