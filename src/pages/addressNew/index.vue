<template>
  <div class="container">
    <van-cell-group>
      <van-field placeholder="收货人" />
      <van-field placeholder="手机号" />
      <van-field placeholder="所在地区" />
      <van-field type="textarea" placeholder="详细地址：如门牌" />
    </van-cell-group>

    <view class="bottomBar">
      <van-button type="default" block>新增地址</van-button>
    </view>
  </div>
</template>

<script>
export default {
  data () {
    return {
      checked: true
    }
  },

  components: {
  },

  computed: {
  },

  methods: {
    onChange({ mp }) {
      // 需要手动对 checked 状态进行更新
      this.checked = mp.detail
    }
  },

  created () {
  },
}
</script>

<style scoped>
.footer {
  display: flex;
  justify-content: space-between;
}
.footer__helper {
  display: flex;
}
.bottomBar {
  position: fixed;
  justify-content: space-between;
  align-items: center;
  width: 100%;
  bottom: 0;
  border-top: 1px gray solid;
  background-color: white;
}
</style>
