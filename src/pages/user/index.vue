<template>
  <div class="container">
    <div class="user-card">
      <image class="user-card__avatar" :src="user.avatar"/>
      <div class="user-card__info">
        <div class="user-card__name">{{ user.name }}</div>
        <div class="user-card__label">
          {{ user.hasCertification?'已认证': '未认证'}}
        </div>
        <div class="user-card__helper">
          <span>注册时间：{{user.registTime}}</span>
          <span style="margin-left: 20rpx;">{{ user.address }}</span>
        </div>
      </div>
    </div>

    <div class="panel">
      <van-cell-group>
        <van-cell title="我发起的团购" value="查看更多" is-link></van-cell>
        <div class="icon-group">
          <div class="icon">
            <div class="iconfont--main icon-user-check"></div>
            <div class="icon__title">发起人认证</div>
          </div>
          <div class="icon">
            <div class="iconfont--main icon-shopping-card"></div>
            <div class="icon__title">商品管理</div>
          </div>
          <div class="icon">
            <div class="iconfont--main icon-users"></div>
            <div class="icon__title">发起团购</div>
          </div>
          <div class="icon">
            <div class="iconfont--main icon-reply"></div>
            <div class="icon__title">待评价</div>
          </div>
        </div>
      </van-cell-group>
    </div>

    <div class="panel">
      <van-cell-group>
        <van-cell title="我的订单" value="查看更多" is-link></van-cell>
        <div class="icon-group">
          <div class="icon">
            <div class="iconfont icon-wallet"></div>
            <div class="icon__title">待付款</div>
          </div>
          <div class="icon">
            <div class="iconfont icon-user-check"></div>
            <div class="icon__title">待发货</div>
          </div>
          <div class="icon">
            <div class="iconfont icon-box"></div>
            <div class="icon__title">待收货</div>
          </div>
          <div class="icon">
            <div class="iconfont icon-reply"></div>
            <div class="icon__title">待评价</div>
          </div>
        </div>
      </van-cell-group>
    </div>

    <div class="panel">
      <van-cell-group>
        <div class="icon-group">
          <div class="icon">
            <div class="iconfont icon-cart-plus"></div>
            <div class="icon__title">商品收藏</div>
          </div>
          <div class="icon">
            <div class="iconfont icon-store"></div>
            <div class="icon__title">店铺收藏</div>
          </div>
          <div class="icon">
            <div class="iconfont icon-edit"></div>
            <div class="icon__title">我的评价</div>
          </div>
          <div class="icon">
            <div class="iconfont icon-redo-alt"></div>
            <div class="icon__title">退款售后</div>
          </div>
          <div class="icon">
            <div class="iconfont icon-cog"></div>
            <div class="icon__title">设置</div>
          </div>
          <div class="icon">
            <div class="iconfont icon-marked-alt"></div>
            <div class="icon__title">收货地址</div>
          </div>
          <div class="icon">
            <div class="iconfont icon-share-alt"></div>
            <div class="icon__title">分享</div>
          </div>
        </div>
      </van-cell-group>
    </div>
  </div>
</template>

<script>
import { mockUserData } from './mock.js'

export default {
  data () {
    return {
      user: {}
    }
  },

  components: {
  },

  methods: {

  },

  created () {
    // get list data
    setTimeout(() => {
      this.user = mockUserData
    }, 500)
  }
}
</script>

<style scoped>
.user-card {
  display: flex;
  padding: 50rpx 20rpx;
  background-color: #FB2525;
}
.user-card__avatar {
  width: 144rpx;
  height: 144rpx;
  border-radius: 50%;
}
.user-card__info {
  padding: 0 30rpx;
  color: #FFFFFF;
}
.user-card__name {
  font-size: 36rpx;
  line-height: 1.4;
}
.user-card__helper {
  font-size: 24rpx;
  line-height: 2;
}
.user-card__label {
  display: inline-block;
  padding: 0 .25em;
  border: 1rpx white solid;
  font-size: 20rpx;
  line-height: 1.6;
}

.panel {
  margin-top: 30rpx;
  background-color: white;
}

.icon-group {
  display: flex;
  justify-content: start;
  flex-wrap: wrap;
}
.icon {
  display: flex;
  flex-direction: column;
  justify-content: center;
  width: 25%;
  padding-bottom: 20rpx;
}
.iconfont,
.iconfont--main {
  display: flex;
  justify-content: center;
  margin: 20rpx 0;
}
.icon ._van-icon {
  display: flex;
  justify-content: center;
  margin: 20rpx 0;
}
.icon__title {
  color: #666666;
  font-size: 26rpx;
  text-align: center;
}

</style>
