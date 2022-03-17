<template>
  <view class="activity-strategy">
    <view class="activity-strategy-body">
        <!-- <li v-for="item in 100">{{item}}</li> -->
        <noDefault></noDefault>
    </view>
  </view>
</template>

<script>
import noDefault from './NoDefault.vue'
export default {
  name: 'ActivityStrategy',
  components: { noDefault }
}
</script>

<style lang='scss' scoped>
.activity-strategy {
  height: 100%;
  padding: 0 24rpx;
  box-sizing: border-box;
  .activity-strategy-body {
    background: white;
    min-height: 100%;
  }

}
</style>
