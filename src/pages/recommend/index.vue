<template>
  <div class="container">
    <div class="tabs-wrap" id="tabs">
      <van-tabs :active="0" @change="onTabsChange">
        <van-tab title="热门"></van-tab>
        <van-tab title="水果"></van-tab>
        <van-tab title="土特产"></van-tab>
        <van-tab title="生鲜"></van-tab>
        <van-tab title="票务"></van-tab>
      </van-tabs>
    </div>

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
        <Card
          v-for="(item, key) in lists" :key="key"
          :cover="item.cover"
          :title="item.title"
          :star="item.star"
          :value="item.value"
          :sold="item.sold"
          :limitDate="item.limitDate"
          :address="item.address"
          :dark="false"
          @onClick="handleCardClick(e, item.id)"
        ></Card>
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

import { mockListData } from './mock.js'

import Card from '@/components/card-list'

export default {
  data () {
    return {
      pageHeight: '',
      tabsHeight: '',

      active: 0,
      lists: []
    }
  },

  components: {
    Card
  },

  computed: {
    scrollViewHeight() {
      console.log(this.tabsHeight)
      return this.pageHeight - this.tabsHeight
    }
  },

  methods: {
    handleScrollToBottom (e) {
      wx.showToast({
        title: `加载更多...`,
        icon: 'none'
      })

      // get list data
      setTimeout(() => {
        this.lists.push(...mockListData)
      }, 500)
    },

    onTabsChange(e) {
      this.active = e.mp.detail.index
      wx.showToast({
        title: `切换到 ${e.mp.detail.title}`,
        icon: 'none'
      })
    }
  },

  created() {
    // get list data
    setTimeout(() => {
      this.lists = mockListData
    }, 500)
  },

  onReady () {
    // set scroll-view height
    getPageHeight(height => this.pageHeight = height)
    getNodeRectHeight('#tabs', rect => {
      this.tabsHeight = rect.height
    })
  }
}
</script>

<style scoped>
.tabs-wrap {
  margin-bottom: 20rpx;
}

scroll-view {
  height: 450px;
}
</style>
