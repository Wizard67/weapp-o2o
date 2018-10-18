<template>
  <div class="container">
    <van-cell-group>
      <van-cell icon="location" is-link>
        <view slot="title">
          <div class="address">
            <div class="address__header">
              <div class="address__name">收货人：张三</div>
              <div class="address__phone">15960123456</div>
            </div>
            <div class="address__body">
              收货地址：北京市丰台区大红门街道珠江骏景北区65号楼1120室
            </div>
          </div>
        </view>
      </van-cell>
    </van-cell-group>

    <div class="panel">
      <van-cell-group>
        <van-cell title="发起人：张三"></van-cell>
        <van-card
          title="山东水蜜桃1.2kg"
          desc="￥ 26.80" 
          num="1"
          price="2.00"
          :thumb="image"
        >
        </van-card>
        <van-cell title="购买数量">
          <slot>
            <van-stepper :value="1" @change="onStepperChange"/>
          </slot>
        </van-cell>
        <van-cell title="物流方式" value="快递免邮" is-link></van-cell>
        <van-cell value="小计：￥ 26.80"></van-cell>
      </van-cell-group>
    </div>

    <view class="bottomBar">
      <van-submit-bar
        :price="2680"
        button-text="提交订单"
        @submit="showCard"
      >
      </van-submit-bar>
    </view>
  </div>
</template>

<script>
export default {
  data () {
    return {
      isCardShow: false,
      image: 'http://img02.tooopen.com/images/20150928/tooopen_sy_143912755726.jpg'
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
