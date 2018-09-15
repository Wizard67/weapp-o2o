<template>
  <div class="container">
    <picker>福州</picker>
    <swiper
      indicator-dots
      autoplay
    >
      <swiper-item>
        <image src="http://img02.tooopen.com/images/20150928/tooopen_sy_143912755726.jpg" class="swiper-image"/>
      </swiper-item>
      <swiper-item>
        <image src="http://img06.tooopen.com/images/20160818/tooopen_sy_175866434296.jpg" class="swiper-image"/>
      </swiper-item>
    </swiper>

    <scroll-view scroll-y style="width: 100%;">
      <van-card
        title="标题"
        desc="描述"  
        num="2"
        price="2.00"
        :thumb="imageURL"
      >
        <view slot="footer">
          <van-button size="mini">按钮</van-button>
          <van-button size="mini">按钮</van-button>
        </view>
      </van-card>
      <van-card
        title="标题"
        desc="描述"  
        num="2"
        price="2.00"
        :thumb="imageURL"
      >
        <view slot="footer">
          <van-button size="mini">按钮</van-button>
          <van-button size="mini">按钮</van-button>
        </view>
      </van-card>
      <van-card
        title="标题"
        desc="描述"  
        num="2"
        price="2.00"
        :thumb="imageURL"
      >
        <view slot="footer">
          <van-button size="mini">按钮</van-button>
          <van-button size="mini">按钮</van-button>
        </view>
      </van-card>
      <van-card
        title="标题"
        desc="描述"  
        num="2"
        price="2.00"
        :thumb="imageURL"
      >
        <view slot="footer">
          <van-button size="mini">按钮</van-button>
          <van-button size="mini">按钮</van-button>
        </view>
      </van-card>
      <van-card
        title="标题"
        desc="描述"  
        num="2"
        price="2.00"
        :thumb="imageURL"
      >
        <view slot="footer">
          <van-button size="mini">按钮</van-button>
          <van-button size="mini">按钮</van-button>
        </view>
      </van-card>
    </scroll-view>
  </div>
</template>

<script>
export default {
  data () {
    return {
      imageURL: 'http://img02.tooopen.com/images/20150928/tooopen_sy_143912755726.jpg'
    }
  },

  components: {
  },

  methods: {

  },

  created () {
  }
}
</script>

<style scoped>
scroll-view {
  height: 400px;
}
.swiper-image {
  width: 100vw;
}
</style>
