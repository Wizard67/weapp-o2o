<note>
  mpvue 的 slot 机制存在问题，部分嵌套组件的使用方式只能折中处理。
  issues: https://github.com/Meituan-Dianping/mpvue/issues/427
</note>

<template>
  <div class="card" :class="{'card--dark': dark}" @click="handleClick">
    <img class="card__cover" :src="cover">
    <div class="card__main">
      <div class="card__title">{{title}}</div>
      <div class="card__info">
        <Star v-if="star" :star="star"/>
        <div style="color: #f44;">￥ {{value}}</div>
        <div>已售 {{sold}}</div>>
      </div>
      <div class="crad__helper">
        <div>截止 {{limitDate}}</div>
        <div>{{address}}</div>
      </div>
    </div>
  </div>
</template>

<script>
import Star from '@/components/star'

export default {
  props: [
    'cover',
    'title',
    'star',
    'dark',
    'value',
    'sold',
    'limitDate',
    'address',
    'onClick'
  ],
  data() {
    return {
    }
  },
  components: {
    Star
  },
  methods: {
    handleClick(e) {
      this.$emit('onClick', e)
    }
  }
}
</script>

<style scoped>
.card {
  position: relative;
  display: flex;
  padding: 20rpx;
}
.card--dark {
  background-color: #efeff4;
}
.card::after {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  width: 200%;
  height: 200%;
  -webkit-transform: scale(.5);
  transform: scale(.5);
  -webkit-transform-origin: 0 0;
  transform-origin: 0 0;
  pointer-events: none;
  box-sizing: border-box;
  border: 0 solid #e5e5e5;
  border-bottom-width: 1px;
}
.card__cover {
  flex: none;
  width: 160rpx;
  height: 160rpx;
  background-color: rgb(245, 245, 245);
}
.card__main {
  width: 100%;
  padding-left: 20rpx;
}

.card__title {
  color: rgb(83, 83, 83);
  font-size: 16px;
  line-height: 1.6;
}
.card__info {
  display: flex;
  justify-content: space-between;
  color: #afafaf;
  font-size: 12px;
  line-height: 2.2;
}
.crad__helper {
  display: flex;
  justify-content: space-between;
  color: #afafaf;
  font-size: 12px;
  line-height: 2;
}
</style>
