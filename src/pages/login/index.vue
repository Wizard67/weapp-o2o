<template>
  <div class="container">
    <van-tabs @change="onTabsChange">
      <van-tab title="密码登录">
        <van-cell-group>
          <van-field
            placeholder="请输入手机号"
            :value="normal.phone"
            :maxlength="11"
            :error="isNormalPhoneError"
            @input="onNormalPhoneChange"
            @blur="checkNormalPhoneValue"
          />
          <van-field
            type="password"
            placeholder="请输入密码"
            :value="normal.password"
            :error="isNormalPasswordError"
            @input="onNormalPasswordChange"
            @blur="checkNormalPasswordValue"
          />
        </van-cell-group>
      </van-tab>

      <van-tab title="短信登录">
        <van-cell-group>
          <van-field
            placeholder="请输入手机号"
            :value="message.phone"
            :error="isMessagePhoneError"
            @input="onMessagePhoneChange"
            @blur="checkMessagePhoneValue"
          />
          <van-field
            placeholder="请输入验证码"
            :value="message.code"
            :error="isMessageCodeError"
            @input="onMessageCodeChange"
            @blur="checkMessageCodeValue"
            use-button-slot
          >
            <van-button
             slot="button" size="mini" type="primary"
             @click="onCodeSend"
             :disabled="isCodeDesabled"
            >{{ codeText }}</van-button>
          </van-field>
        </van-cell-group>
      </van-tab>
    </van-tabs>
    <van-button size="large" @click="onSubmit">登录</van-button>
    <navigator class="text-helper" url="/pages/logup/main">注册</navigator>
  </div>
</template>

<script>
const phoneRegExp = /^1(3|4|5|6|7|8|9)\d{9}$/
const passwordRegExp = /^\S{5,}$/
const codeRegExp = /^\S{4}$/

export default {
  data () {
    return {
      active: 0,

      codeText: '获取验证码',

      // error status
      isNormalPhoneError: false,
      isNormalPasswordError: false,
      isMessagePhoneError: false,
      isMessageCodeError: false,
      isFormError: false,
      isCodeDesabled: false,

      // form data
      normal: {
        phone: '',
        password: ''
      },
      message: {
        phone: '',
        code: ''
      }
    }
  },

  components: {
  },

  methods: {
    setFieldStatus (result, id) {
      if (!result) {
        this.isFormError = true
        this[`is${id}Error`] = true
      } else {
        this.isFormError = false
        this[`is${id}Error`] = false
      }
    },

    // bind date
    onNormalPhoneChange (e) { this.normal.phone = e.mp.detail },
    onNormalPasswordChange (e) { this.normal.password = e.mp.detail },
    onMessagePhoneChange (e) { this.message.phone = e.mp.detail },
    onMessageCodeChange (e) { this.message.code = e.mp.detail },

    // validate
    checkNormalPhoneValue () {
      this.setFieldStatus(phoneRegExp.test(this.normal.phone), 'NormalPhone')
    },
    checkNormalPasswordValue () {
      this.setFieldStatus(passwordRegExp.test(this.normal.password), 'NormalPassword')
    },
    checkMessagePhoneValue () {
      this.setFieldStatus(phoneRegExp.test(this.message.phone), 'MessagePhone')
    },
    checkMessageCodeValue () {
      this.setFieldStatus(codeRegExp.test(this.message.code), 'MessageCode')
    },

    onCodeSend () {
      wx.showToast({
        title: `验证码已发送`
      })
      // Countdown
      const countdown = 60
      const rawText = this.codeText
      this.isCodeDesabled = true

      for (let index = countdown; index >= 0; index--) {
        setTimeout(()=>{
          this.codeText = `已发送（${index}s）`
          if ( index === 0) {
            this.codeText = rawText
            this.isCodeDesabled = false
          }
        }, 1000 * (countdown - index))
      }
    },

    onSubmit () {

      let formDate 

      if (this.active === 0) {
        this.checkNormalPhoneValue()
        this.checkNormalPasswordValue()
        formDate = this.normal
      } else {
        this.checkMessagePhoneValue()
        this.checkMessageCodeValue()
        formDate = this.message
      }

      if (!this.isFormError) {
        wx.showToast({
          title: `发送数据 ${JSON.stringify(formDate)}`,
          icon: 'none'
        })

        // router jump
        setTimeout(()=>{
          wx.switchTab({
            url: '/pages/index/main'
          })
        }, 1000)
      }
    },

    onTabsChange(event) {
      this.active = event.mp.detail.index
      // reset form status
      this.isFormError = false
    }
  }
}
</script>

<style scoped>
.text-helper {
  display: inline-block;
  padding: 12px;
  color: rgb(102, 102, 102);
  font-size: 14px;
}
</style>
