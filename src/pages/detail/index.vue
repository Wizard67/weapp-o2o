<template>
  <div class="container">
    <view class="detail">
      <image class="detail__cover" :src="data.cover" />
      <div class="detail__main">
        <div class="detail__title">{{ data.title }}</div>
        <div class="detail__summary">
          <div class="detail__value">¥{{ data.price/100 }}<span class="detail__count">库存：{{ data.count }}</span></div>
          <div class="detail__views">浏览：{{ data.views }}</div>
        </div>
        <div class="detail__helper">截止时间：{{ data.limitDate }}</div>
      </div>
    </view>

    <div class="panel">
      <van-cell-group>
        <!-- mpvue 用不了模板字符串语法... -->
        <van-cell :title="'发起人：' + data.sponsor"/>
      </van-cell-group>
    </div>

    <template v-for="(item, key) in data.pictures">
      <image class="detail__image" :src="item" :key="key"/>
    </template>

    <view class="bottomBar">
      <van-submit-bar
        button-text="立即购买"
        @submit="showCard"
      >
        <div class="bottomBar__group">
          <span>收藏</span>
          <span>分享</span>
        </div>
      </van-submit-bar>
    </view>

    <van-popup
      position="bottom"
      :show="isCardShow"
      @close="closeCard"
      overlay
    >
      <view class="card">
        <div class="card__summary">
          <image class="card__cover" :src="data.thumbnail"/>
          <div class="card__info">
            <div class="card__value">¥{{ data.price/100 }}</div>
            <span class="card__count">库存：{{ data.conut }}</span>
          </div>
        </div>
        <van-cell-group>
          <van-cell title="购买数量">
            <slot>
              <van-stepper :value="1" :max="data.count" @change="onStepperChange"/>
            </slot>
          </van-cell>
          <van-cell title="物流方式" is-link value="快递免邮" />
          <van-cell :value="'小计 ￥' + value" />
        </van-cell-group>
        <navigator url="/pages/order/main">
          <van-button type="danger" block>确定</van-button>
        </navigator>
      </view>
    </van-popup>
  </div>
</template>

<script>
import { mockDetailData } from './mock.js'

export default {
  data () {
    return {
      isCardShow: false,
      data: {},
      number : 1
    }
  },

  components: {
  },

  computed: {
    value () {
      const price =  this.data.price || 0
      return (price * this.number)/100
    }
  },

  methods: {
    showCard () {
      this.isCardShow = true
    },
    closeCard () {
      this.isCardShow = false
    },
    onStepperChange (e) {
      this.number = e.mp.detail
    }
  },

  created () {
    // get list data
    setTimeout(() => {
      this.data = mockDetailData
    }, 500)
  },
}
</script>

<style scoped>
.detail { }
.detail__cover {
  width: 100%;
  height: 674rpx;
}
.detail__main {
  padding: 20rpx;
  background-color: white;
}
.detail__title {
  font-size: 36rpx;
  color: #333333;
  line-height: 1.6;
}
.detail__summary {
  display: flex;
  justify-content: space-between;
  margin: 20rpx 0;
}
.detail__value {
  color: #FB2525;
  font-size: 36rpx;
}
.detail__count {
  margin-left: 60rpx;
  color: #999999;
  font-size: 24rpx;
}
.detail__views {
  font-size: 24rpx;
  color: #999999;
}
.detail__helper {
  color: #424242;
  font-size: 30rpx;
}

.panel {
  margin: 30rpx 0;
}

.detail__image {
  width: 100%;
}

.bottomBar {
  position: fixed;
  display: flex;
  justify-content: space-between;
  align-items: center;
  width: 100%;
  bottom: 0;
  border-top: 1px gray solid;
  background-color: white;
}
.bottomBar__group {
  display: flex;
  justify-content: space-around;
  width: 100%;
}

.card {
  padding: 20px;
}
.card__summary {
  display: flex;
  align-items: center;
  padding-bottom: 20rpx;
}
.card__cover {
  width: 100px;
  height: 100px;
}
.card__info {
  padding: 20rpx;
}
.card__value {
  color: #FB2525;
  font-size: 36rpx;
}
.card__count {
  color: #999999;
  font-size: 24rpx;
}
</style>
