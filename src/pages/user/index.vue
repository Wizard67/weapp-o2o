<template>
  <div class="container">
    <div class="user-card">
      <image class="user-card__avatar" :src="avatar"/>
      <div class="user-card__info">
        <div>王五</div>
        <div>注册时间：2018-09-19</div>
      </div>
    </div>

    <van-cell-group>
      <van-cell title="我发起的团购" value="查看更多" is-link></van-cell>
      <div class="icon-group">
        <div v-for="item in 4" :key="item">
          <van-icon name="info-o" size="2em"/>
          <div>text</div>
        </div>
      </div>
    </van-cell-group>

    <van-cell-group>
      <van-cell title="我的订单" value="查看更多" is-link></van-cell>
      <div class="icon-group">
        <div v-for="item in 4" :key="item">
          <van-icon name="stop" size="2em"/>
          <div>text</div>
        </div>
      </div>
    </van-cell-group>

    <van-cell-group>
      <div class="icon-group">
        <div v-for="item in 7" :key="item">
          <van-icon name="stop" size="2em"/>
          <div>text</div>
        </div>
      </div>
    </van-cell-group>
  </div>
</template>

<script>
export default {
  data () {
    return {
      avatar: 'http://img02.tooopen.com/images/20150928/tooopen_sy_143912755726.jpg'
    }
  },

  components: {
  },

  methods: {

  },

  created () {
  }
}
</script>

<style scoped>
.user-card {
  display: flex;
  padding: 30rpx;
  background-color: gray;
}
.user-card__avatar {
  width: 100rpx;
  height: 100rpx;
  border-radius: 50%;
}
.user-card__info {
  padding: 0 30rpx;
  color: white;
}

.icon-group {
  display: flex;
  justify-content: space-between;
}

</style>
