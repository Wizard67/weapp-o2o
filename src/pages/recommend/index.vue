<template>
  <div class="container">
    <van-tabs id="tabs" :active="0" @change="onTabsChange">
      <van-tab title="热门"></van-tab>
      <van-tab title="水果"></van-tab>
      <van-tab title="土特产"></van-tab>
      <van-tab title="生鲜"></van-tab>
      <van-tab title="票务"></van-tab>
    </van-tabs>

    <scroll-view
      :style="{height: scrollViewHeight+'px'}"
      lower-threshold="50"
      @scrolltolower="handleScrollToBottom"
      scroll-y
    >
      <van-card
        v-for="item in lists"
        title="原膳翔金鲳鱼340g"
        desc="★★★★★ ￥32.50"
        num="2"
        price="2.00"
        :thumb="item.url"
        :key="item"
      >
        <view class="text-helper" slot="footer">
          仓山万达广场5.9km
        </view>
      </van-card>
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
      tabsHeight: '',

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
      return this.pageHeight - this.tabsHeight
    }
  },

  methods: {
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
    },

    onTabsChange(e) {
      this.active = e.mp.detail.index
      wx.showToast({
        title: `切换到 ${e.mp.detail.title}`,
        icon: 'none'
      })
    }
  },

  created () {
  },

  onReady () {
    // set scroll-view height
    getPageHeight(height => this.pageHeight = height)
    getNodeRectHeight('#tabs', rect => this.pickerHeight = rect.height)
  }
}
</script>

<style scoped>
scroll-view {
  height: 450px;
}
</style>
