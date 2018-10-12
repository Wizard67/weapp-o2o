<template>
  <div class="container">
    <van-row>
      <van-col span="20" offset="2">
        <div class="panel">
          <van-cell-group>
            <van-field
              placeholder="选择收件地址"
              :value="form.address"
              @input="onAddressPhoneChange"
            />
            <picker @change="bindPickerChange" :value="form.poi" :range="pois">
              <van-field
                placeholder="请选择小区"
                :value="form.poi"
              />
            </picker>
          </van-cell-group>
        </div>
      </van-col>
      <van-col span="18" offset="3">
        <div class="button">
          <van-button type="danger" @click="onSubmit">确定</van-button>
          <van-button @click="goToIndex">跳过</van-button>
        </div>
      </van-col>
    </van-row>
  </div>
</template>

<script>
const QQMapWX = require('../../../static/qqmap/qqmap-wx-jssdk.js')

export default {
  data () {
    return {
      pois: [],
      form: {
        address: '',
        poi: ''
      }
    }
  },

  components: {
  },

  methods: {
    bindPickerChange(e) {
      this.form.poi = this.pois[e.mp.detail.value]
    },
    onSubmit() {
      wx.showToast({
        title: `发送表单信息 ${JSON.stringify(this.form)}`,
        icon: 'none'
      })
      setTimeout(()=>{
        wx.switchTab({
          url: '/pages/index/main'
        })
      }, 1000)
    },
    goToIndex() {
      wx.switchTab({
        url: '/pages/index/main'
      })
    }
  },

  onReady() {
    wx.getLocation({
      type: "wgs84",
      success: res => {
        var latitude = res.latitude; // 纬度
        var longitude = res.longitude; // 经度

        const qqmapsdk = new QQMapWX({
          key: "JSDBZ-U4CA2-XUHUH-CX43P-SAXVK-XTFAR"
        })

        // 调用接口
        qqmapsdk.reverseGeocoder({
          location: {
            latitude: latitude,
            longitude: longitude
          },
          get_poi: 1,
          success: res => {
            const pois = []
            res.result.pois.map(item => {
              pois.push(item.title)
            })
            this.form.address = res.result.address
            this.pois = pois
          }
        })
      }
    })
  }
}
</script>

<style scoped>
.panel {
  position: relative;
  top: -60rpx;
  padding: 160rpx 40rpx 0 40rpx;
  background-color: white;
}
.button {
  display: flex;
  justify-content: space-between;
  width: 50%;
  margin: 0 auto;
  padding: 0 80rpx;
}
</style>