<template>
	<view class="help-friends">
		<view class="help-friends-body" v-if="helpList.length">
			<view class="list-item" v-for="(item,index) in helpList" :key="index">
				<text class="index">{{index + 1}}</text>
				<image :src="myImg" class="img"></image>
				<view class="name">
					<view class="name-text">小黄微信昵称</view>
					<view class="item-status">助力失败</view>
				</view>
				<text class="time">11-29 10:39</text>
			</view>
			<!-- <li class="load">加载更多</li> -->
		</view>
		<no-default v-else />
	</view>
</template>

<script>
	import noDefault from './NoDefault.vue'
	export default {
		name: 'helpFriends',
		components: {
			noDefault
		},
		data() {
			return {
				myImg: 'https://img0.baidu.com/it/u=1056811702,4111096278&fm=253&fmt=auto&app=138&f=JPEG?w=500&h=500',
				helpList: [1, 2, 3, 4, 8, 8, 8, 8, 8, 8, 8, 8, 8, 8, 8, 8, 8, 8, 8, 8, 8]
			}
		},
		created() {
			console.log(123)
		}
	}
</script>

<style lang='scss' scoped>
	.help-friends {
		padding: 0 24rpx;
		box-sizing: border-box;
		height: 100%;

		.help-friends-body {
			min-height: 100%;
			background: white;
			padding: 32rpx;
			box-sizing: border-box;
			font-size: 28rpx;

			.load {
				margin-bottom: 150rpx;
				text-align: center;
				width: 100%;
			}

			&>.list-item {
				display: flex;
				align-items: center;
				margin-bottom: 32rpx;
				width: 100%;

				.index {
					color: rgba(51, 51, 51, 0.85);
					margin-right: 24rpx;
				}

				.img {
					width: 60rpx;
					height: 60rpx;
					border-radius: 40rpx;
					margin-right: 24rpx;
				}

				.name {
					flex: 1;
					width: 100%;
					display: flex;
					align-items: center;

					.name-text {
						margin-right: 16rpx;
					}

					.item-status {
						min-width: 110rpx;
						background: #F4F5F8;
						border: 2rpx solid rgba(0, 0, 0, 0.25);
						font-size: 20rpx;
						color: rgba(0, 0, 0, 0.25);
						border-radius: 25rpx;
						padding: 4rpx 15rpx 5rpx 15rpx;
						box-sizing: border-box;
					}
				}

				.time {
					width: 198rpx;
					color: rgba(51, 51, 51, 0.85);
					text-align: right;
				}
			}

			&>.list-item:last-child {
				margin-bottom: 0;
			}
		}
	}
</style>
