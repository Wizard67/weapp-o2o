<template>
  <div class="container">
    <div class="logo">Logo</div>
    <van-row>
      <van-col span="20" offset="2">
        <div class="panel">
          <van-cell-group>
            <van-field
              placeholder="请输入手机号"
              :value="form.phone"
              :maxlength="11"
              :error="isPhoneError"
              @input="onPhoneChange"
              @blur="checkPhoneValue"
            />
            <van-field
              placeholder="请输入验证码"
              :value="form.code"
              :error="isCodeError"
              @input="onCodeChange"
              @blur="checkCodeValue"
              use-button-slot
            >
              <van-button
                type="danger" slot="button" size="mini"
                @click="onCodeSend"
                :disabled="isCodeDesabled"
              >{{ codeText }}</van-button>
            </van-field>

            <van-field
              type="password"
              placeholder="请输入密码"
              :value="form.password"
              :error="isPasswordError"
              @input="onPasswordChange"
              @blur="checkPasswordValue"
            />
          </van-cell-group>
        </div>
      </van-col>
      <van-col span="18" offset="3">
        <div class="button">
          <van-button type="danger" size="large" @click="onSubmit">注册</van-button>
          <div class="helper">
            <div class="text-helper"></div>
            <navigator class="text-helper" url="/pages/login/main">登录</navigator>
          </div>
        </div>
      </van-col>
    </van-row>
  </div>
</template>

<script>
const phoneRegExp = /^1(3|4|5|6|7|8|9)\d{9}$/
const passwordRegExp = /^\S{5,}$/
const codeRegExp = /^\S{4}$/

export default {
  data () {
    return {
      codeText: '获取验证码',

      // error status
      isPhoneError: false,
      isCodeError: false,
      isPasswordError: false,
      isFormError: false,
      isCodeDesabled: false,

      // form data
      form: {
        phone: '',
        code: '',
        password: ''
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

    onPhoneChange (e) { this.form.phone = e.mp.detail },
    onCodeChange (e) { this.form.code = e.mp.detail },
    onPasswordChange (e) { this.form.password = e.mp.detail },

    // validate
    checkPhoneValue () {
      this.setFieldStatus(phoneRegExp.test(this.form.phone), 'Phone')
    },
    checkCodeValue () {
      this.setFieldStatus(codeRegExp.test(this.form.code), 'Code')
    },
    checkPasswordValue () {
      this.setFieldStatus(passwordRegExp.test(this.form.password), 'Password')
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

      this.checkPhoneValue()
      this.checkCodeValue()
      this.checkPasswordValue()

      if (!this.isFormError) {
        wx.showToast({
          title: `发送数据 ${JSON.stringify(this.form)}`,
          icon: 'none'
        })

        // router jump
        setTimeout(()=>{
          wx.redirectTo({
            url: '/pages/login/main'
          })
        }, 1000)
      }
    }
  },

  created () {
  }
}
</script>

<style scoped>
.logo {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 320rpx;
  color: white;
  background-color: #f44;
  font-size: 64rpx;
}
.panel {
  position: relative;
  top: -60rpx;
  padding: 40rpx 40rpx 60rpx 40rpx;
  box-shadow: 0 0 10px 1px rgb(173, 173, 173);
  background-color: white;
}
.button {
  position: relative;
  top: -100rpx;
}
.helper {
  display: flex;
  justify-content: space-between;
}

.text-helper {
  display: inline-block;
  padding: 12px 0;
  color: #f44;
  font-size: 14px;
}
</style>
