<template>
  <view class="invitation-ranking">
     <view class="invitation-ranking-body">
       <!-- <li v-for="item in 100" :key="item" >{{item}}</li> -->
        <no-default :default-text='defaultText' :default-src='defaultSrc' />
     </view>
  </view>
</template>

<script>
import noDefault from './NoDefault.vue'
export default {
  name: 'InvitationRanking',
  components: { noDefault },
  data() {
    return {
      defaultText: '“邀请排名”功能暂未上线，敬请期待～',
      defaultSrc: require('static/images/pm-default.png')
    }
  },
  created() {
    console.log(456)
  }
}
</script>

<style lang='scss' scoped>
.invitation-ranking{
  height: 100%;
  padding: 0 24rpx;
  .invitation-ranking-body {
    background: white;
    min-height: 100%;
  }
}
</style>
