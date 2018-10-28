<template>
  <div class="container">
    <div class="picker-wrap">
      <picker
        id="picker"
        class="fix-picker"
        mode="region"
        :value="region"
        @change="onChangeRegion"
      >{{ region }}</picker>
    </div>

    <swiper
      id="swiper"
      class="fix-swiper"
      autoplay
      circular
    >
      <swiper-item v-for="(item, key) in banners" :key="key+item.id">
        <image :src="item.url" class="swiper-image"/>
      </swiper-item>
    </swiper>

    <scroll-view
      :style="{height: scrollViewHeight * 2 +'rpx'}"
      lower-threshold="50"
      @scrolltolower="handleScrollToBottom"
      scroll-y
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
    </scroll-view>
  </div>
</template>

<script>
const getPageHeight = callback => {
  wx.getSystemInfo({
    success(res) {
      callback(res.windowHeight);
    }
  });
};
const getNodeRectHeight = (nodeId, callback) => {
  wx.createSelectorQuery()
    .select(nodeId)
    .boundingClientRect(rect => callback(rect))
    .exec();
};

const QQMapWX = require("../../../static/qqmap/qqmap-wx-jssdk.min.js");

import { mockBannerData, mockListData } from './mock.js'

import Card from "@/components/card-list";

export default {
  data() {
    return {
      pageHeight: '',
      pickerHeight: '',
      swiperHeight: '',

      region: ['福州'],
      banners: [],
      lists: []
    };
  },

  components: {
    Card
  },

  computed: {
    scrollViewHeight() {
      return this.pageHeight - this.pickerHeight - this.swiperHeight - 10;
    }
  },

  methods: {
    onChangeRegion(e) {
      this.region = e.mp.detail.value[0];
      // reload data
    },

    handleScrollToBottom(e) {
      wx.showToast({
        title: `加载更多...`,
        icon: 'none'
      });

      // get list data
      setTimeout(() => {
        this.lists.push(...mockListData)
      }, 500)
    },

    handleCardClick(e, id) {
      wx.navigateTo({
        url: '/pages/detail/main'
      })
    }
  },

  created() {
    // get user region
    setTimeout(() => {
      this.region = ['北京']
    }, 500)

    // get banner data
    setTimeout(() => {
      this.banners = mockBannerData
    }, 500)

    // get list data
    setTimeout(() => {
      this.lists = mockListData
    }, 500)
  },

  onReady() {
    // set scroll-view height
    getPageHeight(height => (this.pageHeight = height));
    getNodeRectHeight('#picker', rect => (this.pickerHeight = rect.height));
    getNodeRectHeight('#swiper', rect => (this.swiperHeight = rect.height));
  }
};
</script>

<style scoped>
.picker-wrap {
  background-color: white;
}
.fix-picker {
  position: relative;
  display: inline-block;
  padding: 24rpx;
  color: rgb(102, 102, 102);
  background-color: white;
  font-size: 14px;
}
.fix-picker::after {
  position: absolute;
  top: 50%;
  left: 100%;
  transform: translateY(-50%);
  width: 22.4rpx;
  height: 11.2rpx;
  content: "";
  background-image: url(./arrow.png);
  background-size: 100% 100%;
}

.fix-swiper {
  margin-bottom: 20rpx;
}
.swiper-image {
  width: 100vw;
}
</style>
