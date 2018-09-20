<template>
  <div class="container">
    <van-panel title="王五 139****1245" desc="北京市xxx区xxx路" use-footer-slot>
      <view class="footer" slot="footer">
        <van-switch :checked="checked" @change="onChange" />
        <view class="footer__helper">
          <div>编辑</div>
          <div>删除</div>
        </view>
      </view>
    </van-panel>

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
