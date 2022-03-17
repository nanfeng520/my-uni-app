<template>
  <view
    class="content-time"
    v-if="!activityInvalid"
  >
    <view class="djs">活动倒计时</view>
    <view class="line"></view>
    <view class="time-text">{{countDownDateFilter.day}} <span>天</span> </view>
    <view class="line"></view>
    <view class="time-text">{{countDownDateFilter.hour}} <span>时</span> </view>
    <view class="line"></view>
    <view class="time-text">{{countDownDateFilter.min || 0}} <span>分</span> </view>
    <view class="line"></view>
    <view class="time-text">{{countDownDateFilter.second || 0}} <span>秒</span> </view>
  </view>
</template>

<script>
export default {
  name: 'ActivityCountdown',
  props: {
    activityInvalid: { // true表示活动过期
      type: Boolean,
      default: () => false
    },
    endTime: {
      type: String,
      default: () => ''
    }
  },
  data() {
    return {
      countDownDate: {
        day: 0,
        hour: 0,
        min: 0,
        second: 0
      },
      endTimetamp: ''
    }
  },
  // watch: {
  //   endTime(val) {
  //     console.log('======' + val)
  //     this.countdownStart(val)
  //   }
  // },
  mounted(){
	  console.log('---endTime')
	  this.countdownStart(this.endTime)
  },
  computed: {
    countDownDateFilter() {
      return {
        day: this.countDownDate.day <= 0 ? 0 : this.countDownDate.day,
        hour: this.countDownDate.hour <= 0 ? 0 : this.countDownDate.hour,
        min: this.countDownDate.min <= 0 ? 0 : this.countDownDate.min,
        second: this.countDownDate.second <= 0 ? 0 : this.countDownDate.second
      }
    }
  },
  created(){
	  console.log('gg===============')
  },
  methods: {
    mySetInterval (cb, cancelCb) {
      let timer = null
      let pre = new Date()
      let fn = () => {
        timer = requestAnimationFrame(() => {
          let cur = new Date()
          if (cur - pre >= 1000) {
            cb()
            pre = cur
          }
          timer = requestAnimationFrame(fn)
          if (cancelCb && cancelCb()) {
            console.log('活动到期')
            uni.$emit('activityInvalidFn')
            timer && cancelAnimationFrame(timer)
          }
        })
      }
      fn()
    },
    countdownStart (endTime) {
      this.endTimetamp = new Date(endTime).getTime()
      // console.log(endTime, this.endTimetamp)
      this.mySetInterval(this.countDown, this.cancel)
    },
    countDown () {
      let dis = (this.endTimetamp - new Date().getTime()) / 1000
      this.countDownDate = this.calculator(dis)
      console.log('发送事件---->', this.countDownDate)
    },
    cancel () {
      return !!(this.countDownDate && this.countDownDate.timetamp <= 0)
    },
    calculator (second) {
      let sec = 1
      let min = 60 * sec
      let hour = 60 * min
      let day = 24 * hour
      return {
        day: parseInt(second / day),
        hour: parseInt(second % day / hour),
        min: parseInt(second % hour / min),
        second: parseInt(second % min),
        timetamp: second
      }
    }
  }
}
</script>

<style lang='scss' scoped>
.content-time {
  width: 100%;
  padding: 0 12rpx 0 10rpx;
  box-sizing: border-box;
  height: 64rpx;
  background: url("~@/static/images/time-back.png") no-repeat;
  background-size: 100% 100%;
  border-radius: 16rpx;
  display: flex;
  align-items: center;
  justify-content: space-around;
  margin-bottom: 80rpx;
  .djs {
    font-size: 20rpx;
    font-weight: 400;
    color: rgba(0, 0, 0, 0.25);
  }
  .line {
    height: 16rpx;
    background: #ff8d4d;
    color: #ff8d4d;
    opacity: 1;
    border: 1rpx solid rgba(0, 0, 0, 0.85);
  }
  .time-text {
    font-size: 36rpx;
    color: #ff8d4d;
    font-weight: 600;
    width: 82rpx;
    & > span {
      font-size: 20rpx;
      color: rgba(0, 0, 0, 0.25);
      font-weight: 400;
    }
  }
}
</style>
