<template>
  <div class="container">
    <van-cell-group>
      <van-cell icon="location" is-link>
        <view slot="title">
          <view>收货人：张三  1888888888</view>
          <view>收货地址：北京市丰台区某路某街xx楼xx号</view>
        </view>
      </van-cell>
    </van-cell-group>

    <van-cell-group>
      <van-cell title="发起人：张三"></van-cell>
      <van-card
        title="山东水蜜桃1.2kg"
        desc="￥250"  
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
      <van-cell value="小计：￥250"></van-cell>
    </van-cell-group>

    <view class="bottomBar">
      <text class="bottomBar__text">合计：￥250</text>
      <van-button type="default" @click="showCard">立即购买</van-button>
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
</style>
