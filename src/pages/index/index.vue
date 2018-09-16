<template>
  <div class="container">
    <picker
      id="picker"
      class="text-helper"
      mode="region"
      :value="region"
      @change="onChangeRegion"
    >{{ region }}</picker>
    <swiper
      id="swiper"
      indicator-dots
      autoplay
      circular
    >
      <swiper-item v-for="(item, key) in banners" :key="key+item.id">
        <image :src="item.url" class="swiper-image"/>
      </swiper-item>
    </swiper>

    <scroll-view
      :style="{height: scrollViewHeight+'px'}"
      lower-threshold="50"
      @scrolltolower="handleScrollToBottom"
      scroll-y
    >
      <navigator
        v-for="item in lists"
        url="/pages/detail/main"
        :key="item"
      >
        <van-card
          title="原膳翔金鲳鱼340g"
          desc="★★★★★ ￥32.50"
          num="2"
          price="2.00"
          :thumb="item.url"
        >
        <view class="text-helper" slot="footer">
          仓山万达广场5.9km
        </view>
      </van-card>
      </navigator>
    </scroll-view>
  </div>
</template>

<script>
const getPageHeight = callback => {
  wx.getSystemInfo({success(res) {callback(res.windowHeight)}})
}
const getNodeRectHeight = (nodeId, callback) => {
  wx.createSelectorQuery().select(nodeId).boundingClientRect(rect => callback(rect)).exec()
}

export default {
  data () {
    return {
      pageHeight: '',
      pickerHeight: '',
      swiperHeight: '',

      region: ['福州'],
      banners: [
        { url: 'http://img02.tooopen.com/images/20150928/tooopen_sy_143912755726.jpg', id: 1 },
        { url: 'http://img06.tooopen.com/images/20160818/tooopen_sy_175866434296.jpg', id: 2 },
        { url: 'http://img02.tooopen.com/images/20150928/tooopen_sy_143912755726.jpg', id: 3 }
      ],

      lists: [
        { url: 'http://img02.tooopen.com/images/20150928/tooopen_sy_143912755726.jpg', id: 1 },
        { url: 'http://img02.tooopen.com/images/20150928/tooopen_sy_143912755726.jpg', id: 2 },
        { url: 'http://img02.tooopen.com/images/20150928/tooopen_sy_143912755726.jpg', id: 3 },
        { url: 'http://img02.tooopen.com/images/20150928/tooopen_sy_143912755726.jpg', id: 4 },
        { url: 'http://img02.tooopen.com/images/20150928/tooopen_sy_143912755726.jpg', id: 5 },
        { url: 'http://img02.tooopen.com/images/20150928/tooopen_sy_143912755726.jpg', id: 6 },
        { url: 'http://img02.tooopen.com/images/20150928/tooopen_sy_143912755726.jpg', id: 7 },
      ]
    }
  },

  components: {
  },

  computed: {
    scrollViewHeight() {
      return this.pageHeight - this.pickerHeight - this.swiperHeight
    }
  },

  methods: {

    onChangeRegion (e) {
      this.region = e.mp.detail.value[0]
      // reload data
    },

    handleScrollToBottom (e) {
      wx.showToast({
        title: `加载更多...`,
        icon: 'none'
      })
      this.lists.push(
        { url: 'http://img02.tooopen.com/images/20150928/tooopen_sy_143912755726.jpg', id: 1 },
        { url: 'http://img02.tooopen.com/images/20150928/tooopen_sy_143912755726.jpg', id: 2 },
        { url: 'http://img02.tooopen.com/images/20150928/tooopen_sy_143912755726.jpg', id: 3 }
      )
    }
  },

  created () {
  },

  onReady () {
    // set scroll-view height
    getPageHeight(height => this.pageHeight = height)
    getNodeRectHeight('#picker', rect => this.pickerHeight = rect.height)
    getNodeRectHeight('#swiper', rect => this.swiperHeight = rect.height)
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

scroll-view {
  height: 400px;
}
.swiper-image {
  width: 100vw;
}
</style>
