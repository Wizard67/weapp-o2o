<template>
  <div class="star-group">
    <span v-for="(i,k) in correctStar" class="star" :key="k">★</span>&nbsp;
    {{correctStar === 0? '暂无评价': correctStar}}
  </div>
</template>

<script>
export default {
  props: {
    star: Number
  },
  computed: {
    correctStar() {
      return [0, 1, 2, 3, 4, 5].indexOf(this.star) !== -1? this.star: 0
    }
  }
}
</script>

<style scoped>
.star-group {
  display: flex;
  align-items: center;
  width: 240rpx;
  color: #afafaf;
  font-size: 12px;
  line-height: 2.2;
  overflow: hidden;
}
.star {
  flex: 0;
  height: 1.1em;
  margin: 0 5rpx;
  padding: 0 0.1em;
  border-radius: 6rpx;
  color: white;
  background-color: #f44;
  font-size: 12px;
  line-height: 1.1em;
}
</style>
