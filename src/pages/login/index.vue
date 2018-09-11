<template>
  <div class="container">
    <van-tabs @change="onTabsChange">
      <van-tab title="密码登录">
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
            placeholder="请输入密码"
            :border="false"
            @change="onChange"
            :error="false"
          />
        </van-cell-group>
      </van-tab>

      <van-tab title="短信登录">
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
        </van-cell-group>
      </van-tab>
    </van-tabs>
    <van-button size="large">登录</van-button>
    <navigator url="/pages/logup/main">注册</navigator>
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
