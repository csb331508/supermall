<template>
  <div class="recommend">
    <div v-for="item in recommends" class="recommendItem">
      <a :href="item.link">
        <img :src="item.image" alt="" />
      </a>
      <div>{{ item.title }}</div>
    </div>
  </div>
</template>

<script>
export default {
  name: "RecommendView",
  props: {
    recommends: {
      type: Array,
      default() {
        return [];
      },
    },
  },
};
</script>

<style scoped>
.recommend {
  width: 375px;
  display: flex;
  text-align: center;
  font-size: 13px;
  padding: 10px 0 30px;
  border-bottom: 10px solid #eee;
}
.recommendItem {
  flex: 1;
}
.recommendItem img {
  width: 70px;
}
</style>