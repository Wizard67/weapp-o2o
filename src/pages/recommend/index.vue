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

import Card from '@/components/card-list'

export default {
  data () {
    return {
      pageHeight: '',
      tabsHeight: '',

      lists: [
        {
          id: 1,
          cover: 'http://img02.tooopen.com/images/20150928/tooopen_sy_143912755726.jpg',
          title: '原膳泰翔二去金昌鱼340kg',
          star: 5,
          value: 32.90,
          sold: 5000,
          limitDate: '2018-08-24',
          daaress: '仓山万达广场5.9km'
        },
        {
          id: 2,
          cover: 'http://img02.tooopen.com/images/20150928/tooopen_sy_143912755726.jpg',
          title: '原膳泰翔二去金昌鱼340kg',
          star: 5,
          value: 32.90,
          sold: 5000,
          limitDate: '2018-08-24',
          daaress: '仓山万达广场5.9km'
        },
        {
          id: 3,
          cover: 'http://img02.tooopen.com/images/20150928/tooopen_sy_143912755726.jpg',
          title: '原膳泰翔二去金昌鱼340kg',
          star: 5,
          value: 32.90,
          sold: 5000,
          limitDate: '2018-08-24',
          daaress: '仓山万达广场5.9km'
        },
        {
          id: 4,
          cover: 'http://img02.tooopen.com/images/20150928/tooopen_sy_143912755726.jpg',
          title: '原膳泰翔二去金昌鱼340kg',
          star: 5,
          value: 32.90,
          sold: 5000,
          limitDate: '2018-08-24',
          daaress: '仓山万达广场5.9km'
        },
        {
          id: 5,
          cover: 'http://img02.tooopen.com/images/20150928/tooopen_sy_143912755726.jpg',
          title: '原膳泰翔二去金昌鱼340kg',
          star: 5,
          value: 32.90,
          sold: 5000,
          limitDate: '2018-08-24',
          daaress: '仓山万达广场5.9km'
        }
      ]
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
      this.lists.push(
        {
          id: 6,
          cover: 'http://img02.tooopen.com/images/20150928/tooopen_sy_143912755726.jpg',
          title: '原膳泰翔二去金昌鱼340kg',
          star: 5,
          value: 32.90,
          sold: 5000,
          limitDate: '2018-08-24',
          daaress: '仓山万达广场5.9km'
        }
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
    getNodeRectHeight('#tabs', rect => {
      this.tabsHeight = rect.height
    })
  }
}
</script>

<style scoped>
scroll-view {
  height: 450px;
}
</style>
