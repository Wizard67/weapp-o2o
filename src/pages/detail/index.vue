<template>
  <div class="container">
    <view class="detail">
      <image class="detail__image" src="http://img02.tooopen.com/images/20150928/tooopen_sy_143912755726.jpg" />
      <text class="detail__text">山东水蜜桃</text>
      <text class="detail__text">￥26.80</text>
      <text class="detail__text">截止时间： 2018-08-31</text>
    </view>

    <van-cell-group>
      <van-cell title="发起人：王五"/>
    </van-cell-group>

    <image class="detail__image" src="http://img06.tooopen.com/images/20160818/tooopen_sy_175866434296.jpg" />

    <view class="bottomBar">
      <text class="bottomBar__text">收藏</text>
      <text class="bottomBar__text">分享</text>
      <van-button type="default" @click="showCard">立即购买</van-button>
    </view>

    <van-popup
      position="bottom"
      :show="isCardShow"
      @close="closeCard"
      overlay
    >
      <view class="card">
        <image class="card__image" src="http://img06.tooopen.com/images/20160818/tooopen_sy_175866434296.jpg"/>
        <van-cell-group>
          <van-cell title="物流方式" is-link value="快递免邮" />
          <van-cell title="购买数量">
            <slot>
              <van-stepper :value="1" @change="onStepperChange"/>
            </slot>
          </van-cell>
          <van-cell value="小计 ￥200" />
        </van-cell-group>
        <navigator url="/pages/order/main">
          <van-button type="default" block>确定</van-button>
        </navigator>
      </view>
    </van-popup>
  </div>
</template>

<script>
export default {
  data () {
    return {
      isCardShow: false
    }
  },

  components: {
  },

  computed: {
  },

  methods: {
    showCard () {
      this.isCardShow = true
    },
    closeCard () {
      this.isCardShow = false
    },
    onStepperChange () {

    }
  },

  created () {
  },
}
</script>

<style scoped>
.text-helper {
  display: inline-block;
  padding: 12px;
  color: rgb(102, 102, 102);
  font-size: 14px;
}
.detail__image {
  width: 100%;
}
.detail__text {
  display: block;
  padding: 5px;
  font-size: 14px;
  color: rgb(102, 102, 102);
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
.bottomBar__text {
  padding: 5px;
  font-size: 14px;
  color: rgb(102, 102, 102);
}

.card {
  padding: 20px;
}
.card__image {
  width: 100px;
  height: 100px;
}
</style>
