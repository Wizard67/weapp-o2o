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

import Card from "@/components/card-list";

export default {
  data() {
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
        {
          id: 1,
          cover: 'http://img02.tooopen.com/images/20150928/tooopen_sy_143912755726.jpg',
          title: '原膳泰翔二去金昌鱼340kg',
          star: 5,
          value: 32.90,
          sold: 5000,
          limitDate: '2018-08-24',
          address: '仓山万达广场5.9km'
        },
        {
          id: 2,
          cover: 'http://img02.tooopen.com/images/20150928/tooopen_sy_143912755726.jpg',
          title: '原膳泰翔二去金昌鱼340kg',
          star: 5,
          value: 32.90,
          sold: 5000,
          limitDate: '2018-08-24',
          address: '仓山万达广场5.9km'
        },
        {
          id: 3,
          cover: 'http://img02.tooopen.com/images/20150928/tooopen_sy_143912755726.jpg',
          title: '原膳泰翔二去金昌鱼340kg',
          star: 5,
          value: 32.90,
          sold: 5000,
          limitDate: '2018-08-24',
          address: '仓山万达广场5.9km'
        },
        {
          id: 4,
          cover: 'http://img02.tooopen.com/images/20150928/tooopen_sy_143912755726.jpg',
          title: '原膳泰翔二去金昌鱼340kg',
          star: 5,
          value: 32.90,
          sold: 5000,
          limitDate: '2018-08-24',
          address: '仓山万达广场5.9km'
        },
        {
          id: 5,
          cover: 'http://img02.tooopen.com/images/20150928/tooopen_sy_143912755726.jpg',
          title: '原膳泰翔二去金昌鱼340kg',
          star: 5,
          value: 32.90,
          sold: 5000,
          limitDate: '2018-08-24',
          address: '仓山万达广场5.9km'
        }
      ]
    };
  },

  components: {
    Card
  },

  computed: {
    scrollViewHeight() {
      console.log(this.swiperHeight)
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
      this.lists.push(
        {
          id: 6,
          cover: 'http://img02.tooopen.com/images/20150928/tooopen_sy_143912755726.jpg',
          title: '原膳泰翔二去金昌鱼340kg',
          star: 5,
          value: 32.90,
          sold: 5000,
          limitDate: '2018-08-24',
          address: '仓山万达广场5.9km'
        }
      );
    },

    handleCardClick(e, id) {
      wx.navigateTo({
        url: '/pages/detail/main'
      })
    }
  },

  created() {},

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
