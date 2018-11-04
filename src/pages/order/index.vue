<template>
  <div class="container">
    <van-cell-group>
      <van-cell icon="location" is-link>
        <view slot="title">
          <div class="address">
            <div class="address__header">
              <div class="address__name">收货人：{{ address.name }}</div>
              <div class="address__phone">{{ address.phone }}</div>
            </div>
            <div class="address__body">
              收货地址：{{ address.address }}
            </div>
          </div>
        </view>
      </van-cell>
    </van-cell-group>

    <div class="panel">
      <van-cell-group>
        <van-cell :title="'发起人：' + order.sponsor"></van-cell>
        <van-card
          :title="order.title"
          :desc="order.desc" 
          :num="order.number"
          :price="order.price/100"
          :thumb="order.thumbnail"
        >
        </van-card>
        <van-cell title="购买数量">
          <slot>
            <van-stepper :value="order.number" :min="order.number" :max="order.number" disabled/>
          </slot>
        </van-cell>
        <van-cell title="物流方式" :value="order.transport" is-link></van-cell>
        <van-cell :value="'小计：￥'+ (order.value/100)"></van-cell>
      </van-cell-group>
    </div>

    <view class="bottomBar">
      <van-submit-bar
        :loading="isLoading"
        :price="order.value"
        button-text="提交订单"
        @submit="submitForm"
      >
      </van-submit-bar>
    </view>
  </div>
</template>

<script>
import { mockcommonAddressData, mockOrderData } from './mock.js'

export default {
  data () {
    return {
      isLoading: false,

      address: {},
      order: {}
    }
  },

  components: {
  },

  computed: {
  },

  methods: {
    submitForm() {
      this.isLoading = true
      setTimeout(()=>{
        this.isLoading = false
      }, 3000)
    }
  },

  created () {
    // get list data
    setTimeout(() => {
      this.address = mockcommonAddressData
    }, 500)

    // get list data
    setTimeout(() => {
      this.order = mockOrderData
    }, 500)
  }
}
</script>

<style scoped>
.address {
  padding: 0 10rpx;
}
.address__header {
  display: flex;
  justify-content: space-between;
  color: #333333;
  font-size: 30rpx;
}
.address__body {
  padding: 10rpx 0;
  font-size: 24rpx;
  line-height: 1.6;
}

.panel {
  margin: 30rpx 0;
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
</style>
