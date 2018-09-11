<template>
  <div class="container">
    <van-cell-group>
      <van-field
        :value="phone"
        placeholder="请输入手机号"
        :border="false"
        @change="onChange"
        :error="false"
      />
      <van-field
        :value="password"
        type="password"
        placeholder="请输入验证码"
        :border="false"
        @change="onChange"
        use-button-slot
        :error="false"
      >
        <van-button slot="button" size="mini" type="primary">获取验证码</van-button>
      </van-field>

      <van-field
        :value="password"
        type="password"
        placeholder="请输入密码"
        :border="false"
        @change="onChange"
        :error="false"
      />
    </van-cell-group>
    <van-button size="large">注册</van-button>
    <navigator url="/pages/login/main">登录</navigator>
  </div>
</template>

<script>
import card from '@/components/card'

export default {
  data () {
    return {
      active: 0,
      phone: '',
      password: ''
    }
  },

  components: {
    card
  },

  methods: {
    clickHandle (msg, ev) {
      console.log('clickHandle:', msg, ev)
    },
    onTabsChange(event) {
      this.active = event.mp.detail.index
      wx.showToast({
        title: `切换到 tab ${event.mp.detail.index}`,
        icon: 'none'
      });
    }
  },

  created () {
  }
}
</script>

<style scoped>

</style>
