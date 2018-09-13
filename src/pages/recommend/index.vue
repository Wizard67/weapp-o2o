<template>
  <div class="container">
    <van-tabs :active="0">
      <van-tab title="热门">
        <scroll-view scroll-y style="width: 100%;">
        <van-card
          title="标题"
          desc="描述"  
          num="2"
          price="2.00"
          :thumb="imageURL"
          v-for="i in 5"
          :key="i"
        >
          <view slot="footer">
            <van-button size="mini">按钮</van-button>
            <van-button size="mini">按钮</van-button>
          </view>
        </van-card>
        </scroll-view>
      </van-tab>
      <van-tab title="水果">内容 2</van-tab>
      <van-tab title="土特产">内容 3</van-tab>
      <van-tab title="生鲜">内容 4</van-tab>
      <van-tab title="票务">内容 5</van-tab>
    </van-tabs>
  </div>
</template>

<script>
import card from '@/components/card'

export default {
  data () {
    return {
      imageURL: 'http://img02.tooopen.com/images/20150928/tooopen_sy_143912755726.jpg'
    }
  },

  components: {
    card
  },

  methods: {

  },

  created () {
  }
}
</script>

<style scoped>
scroll-view {
  height: 450px;
}
</style>
