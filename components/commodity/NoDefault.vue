<template>
  <view class="fission-no-default">
    <view class="default-body">
	  <image class="default-img" :src="defaultSrc"></image>
      <view class="text">{{ defaultText }}</view>
    </view>
  </view>
</template>

<script>
export default {
  name: 'FissionNoDefault',
  props: {
    defaultText: {
      type: String,
      default: () => '暂无助力好友，快去邀请好友来助力吧～'
    },
    defaultSrc: {
      type: String,
      default: () => require('static/images/no-default.png')
    }
  }
}
</script>

<style lang='scss' scoped>
.fission-no-default {
  height: 100%;
  background: white;
  padding-top: 80rpx;
  box-sizing: border-box;
  .default-body {
    text-align: center;
    & > .default-img {
      width: 178rpx;
      height: 158rpx;
    }
    & > .text {
      margin-top: 48rpx;
      font-size: 24rpx;
      font-weight: 400;
      color: rgba(0, 0, 0, 0.35);
    }
  }
}
</style>
