<template>
  <view class="fission-home">
    <view id="fission-body">
        <!-- 用户卡片信息 -->
      <user-card-info
        :activity-invalid='activityInvalid'
        :endTime='endTime'
       ></user-card-info>
      <!-- tabs -->
      <view id="fission-tabs">
        <view id="ul-tabs-padding">
          <view id="ul-tabs">
            <view 
				class='ul-tabs-li' 
				v-for="item in tabList" 
				:key="item.type"
                :class="{'tabs-active':item.type === tabsActive}"
                @click="handleTabs(item.type)">
				<image 
					class="tabs-li-icon"
					v-if="item.type === tabsActive" :src="getTabsIcon(item.type)"></image>
				{{item.name}}
            </view>
          </view>
        </view>
        <!-- 占位符 placeholder，滚动时候tabs会变成固定定位，占位符为了保持平滑 -->
        <view id="tabs-placeholder"></view>
        <!-- v-if="tabsShow" v-if的逻辑已经写好，需要时放开 -->
        <component :is='tabsName' ></component>
      </view>
    </view>
    <view class="invite-friends">
		<button type="primary" :class="{'disabled-btn':activityInvalid}" >
			 {{ activityInvalid ? '本次活动已结束':'邀请好友助力'}}
		</button>
    </view>
    <!-- <van-overlay :show="overlayShow">
      <view class="wrapper" @click.stop>
        <img src="./images/code.png">
        <view class="block">123</view>
      </view>
    </van-overlay> -->
  </view>
</template>

<script>
import UserCardInfo from 'components/commodity/UserCardInfo.vue'
import HelpFriends from 'components/commodity/HelpFriends.vue'
import InvitationRanking from 'components/commodity/InvitationRanking.vue'
import ActivityStrategy from 'components/commodity/ActivityStrategy.vue'
let tabsOffsetTop = 0
let tabsNameData = {
  1: 'HelpFriends',
  2: 'InvitationRanking',
  3: 'ActivityStrategy'
}
export default {
  name: 'fissionIndex',
  // HelpFriends, InvitationRanking, ActivityStrategy
  components: { UserCardInfo ,HelpFriends,InvitationRanking,ActivityStrategy},
  data() {
    return {
      tabsName: 'HelpFriends', // component 动态组件名name
      activityInvalid: false, // true表示活动过期
      tabList: [
        { name: '助力好友', type: 1 },
        { name: '邀请排名', type: 2 },
        { name: '活动攻略', type: 3 }
      ],
      tabsActive: 1, // 选中的tab
      isSticky: false, // 吸顶tabs
      endTime: '', // 过期时间
      overlayShow: true
    }
  },
  onLoad(){
	   window.addEventListener('scroll', this.handleScroll, true)
	   uni.$on('activityInvalidFn', () => {
	     this.activityInvalid = true
	   })
	   this.endTime = '2022/05/26 12:28:10'
  },
  onUnload(){
	 uni.$off('activityInvalidFn')
  },
  onPageScroll(e){
	  let htmlTop = e.scrollTop
	  let tabsDiv = document.querySelector('#ul-tabs-padding') // 元素距离顶部距离
	  console.log(tabsDiv.offsetTop)
	  let tabsPlaceholder = document.querySelector('#tabs-placeholder') // tabs占位符
	  if (!tabsOffsetTop) tabsOffsetTop = tabsDiv.offsetTop
	  // console.log(htmlTop + '=========' + tabsOffsetTop)
	  if (htmlTop >= tabsOffsetTop) { // 开启吸顶状态
	    tabsDiv.style.position = 'fixed'
	    tabsDiv.style.top = 44 + 'px'
	    tabsPlaceholder.style.display = 'block'
	    this.isSticky = true
	  } else {
	    this.isSticky = false
	    tabsPlaceholder.style.display = 'none'
	    tabsDiv.style.position = 'static'
	  }
  },
  methods: {
    tabsShow() {
      let tabsActive = tabsNameData[this.tabsActive]
      return tabsActive === this.tabsName
    },
    handleTabs(type) {
      if (this.tabsName === tabsNameData[type]) return
      this.tabsActive = type
      this.tabsName = tabsNameData[type]
      if (this.isSticky) { // 吸顶状态每次切换调整距离顶端距离
        document.querySelector('#fission-body').scrollTop = tabsOffsetTop
      }

      // tabsOffsetTop
    },
    getTabsIcon(type) {
      let obj = {
        1: require('static/images/tabs-1.png'),
        2: require('static/images/tabs-2.png'),
        3: require('static/images/tabs-3.png')
      }
      return obj[type]
    },
    handleScroll() {
		
    }
  }
}
</script>


<style lang='scss'>
 .fission-home{
   width: 100%;
   height: 100%;
   display: flex;
   flex-direction: column;
   .van-overlay {
     z-index: 99;
     .wrapper {
       height: 100%;

       .block {
         color: black;
         width: 50vw;
         height: 50vh;
         background: white;
       }
     }
   }
   #fission-body {
      height: 100%;
      overflow-y: auto;
      display: flex;
      flex-direction: column;
      #fission-tabs {
        width: 100%;
        height: 100%;
        //  padding: 0px 24rpx;
        box-sizing: border-box;
        display: flex;
        flex-direction: column;
        #tabs-placeholder {
          min-height: 96rpx;
          display: none;
        }
        #ul-tabs-padding {
          padding: 32rpx 0rpx 0rpx 24rpx;
          box-sizing: border-box;
          width: 100%;
          background: #EEF0F5;
		  z-index: 99;
        }
        #ul-tabs {
          height: 64rpx;
          width: 100%;
          display: flex;
          align-items: center;
          background: #EAEBEE;
          border-radius: 12rpx 12rpx 0 0;
          & > .ul-tabs-li {
            flex-basis: 31.2%;
            //  background: #EAEBEE;
            //  text-align: center;
            height: 100%;
            font-size:28rpx;
            color: #595959;
            font-weight: 400;
            display: flex;
            align-items: center;
            justify-content: center;
			.tabs-li-icon {
				margin-right: 12rpx;
				width: 30rpx;
				height: 30rpx;
			}
          }
          & > .ul-tabs-li:first-child {
            border-radius: 12rpx 0 0 0;
          }
          & > .ul-tabs-li:last-child {
            border-radius: 0 12rpx 0 0;
          }
          > .tabs-active {
              flex-basis: 37.6%;
              background: white;
              font-weight: 600;
              color: #262626;
              border-radius: 12rpx 12rpx 0 0;
          }
        }
    }
   }
  .invite-friends {
    padding:46rpx 48rpx 0rpx 48rpx;
    box-sizing: border-box;
    width: 100%;
    height:192rpx;
    background: #FFFFFF;
    border-radius: 0px 0px 24rpx 24rpx;
	& > button {
      width: 100%;
      background: linear-gradient(90deg, #FF8D4D 0%, #FF5739 100%);
      border-radius: 50rpx;
      font-weight: 500;
      color: #FFFFFF;
      font-size: 32rpx;
    }
    .disabled-btn {
      background: #CDCDCD;
    }
  }

 }
</style>

