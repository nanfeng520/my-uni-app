<template>
	<view class="card-info" :class="{'header-bottom':activityInvalid}">
		<view class="header-info">
			<image :src="myImg" class="h-img"></image>
			<view class="h-name">
				<view class="name-prize">
					<view class="name">此处微信昵称</view>
					<view class="my-prize" @click="handleMyPrize">
						<view class="prize">我的奖品</view>
					</view>
				</view>
				<view class="pm">
					<view>排名112</view>
					<view class="cumulative-invitation">累计邀请：112人</view>
				</view>
			</view>
		</view>
		<view class="gift-body" :class="{'activity-invalid':activityInvalid}">
			<view class="gift-c-li">
				<view></view>
			</view>
			<view class="gift-c-li">
				<view></view>
			</view>
			<view class="gift-c-li">
				<view></view>
			</view>
			<view class="gift-c-li">
				<view class="gift-active">
					<view class="active-content">
						<!-- 倒计时 -->
						<activity-countdown v-if="!activityInvalid" :activityInvalid='activityInvalid' :endTime='endTime' />
						<view class="content-gift">
							<view class="progress-bar"></view>
							<view class="gift-one" :style="{left:giftProgressWidth(item)}" v-for="item in giftList" :key="item">
								<image :src="giftActive" class="gift-img"></image>
							</view>
						</view>
						<view class="content-result">
							已邀请<span>25人</span>，您还差 <span>9个</span>人完成任务
						</view>
					</view>
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	import ActivityCountdown from './ActivityCountdown.vue'
	export default {
		name: 'UserCardInfo',
		components: {
			ActivityCountdown
		},
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
				giftActive: require('static/images/gift-active.png'),
				giftNoActive: require('static/images/gift-no-active.png'),
				giftList: [1], // 奖品数量
				myImg: 'https://img0.baidu.com/it/u=1056811702,4111096278&fm=253&fmt=auto&app=138&f=JPEG?w=500&h=500'

			}
		},
		methods: {
			giftProgressWidth(i) {
				let pre = 90 / this.giftList.length
				return pre * i + '%'
			},
			handleMyPrize() {
				this.$router.push({
					path: '/myPrize'
				})
			}
		}
	}
</script>

<style scoped lang='scss'>
	.card-info {
		width: 100%;
		margin-bottom: 250rpx; //282

		.gift-body {
			// height: 100%;
			width: 100%;
			position: relative;

			& > .gift-c-li {
				position: absolute;
				width: 100%;
				box-sizing: border-box;
				height: 332rpx; //活动过期 332 236

				> view {
					width: 100%;
					height: 100%;
					background: #ffffff;
					border-radius: 10rpx;
				}
			}

			& > .gift-c-li:nth-child(1) {
				top: -120rpx;
				z-index: 1;
				padding: 0px 60rpx;
				opacity: 0.2;
			}

			& > .gift-c-li:nth-child(2) {
				top: -112rpx;
				z-index: 2;
				padding: 0px 52rpx;
				opacity: 0.4;
			}

			& > .gift-c-li:nth-child(3) {
				top: -100rpx;
				z-index: 3;
				padding: 0px 44rpx;
				opacity: 0.4;
			}

			& > .gift-c-li:nth-child(4) {
				top: -88rpx;
				padding: 0px -32rpx;
				z-index: 4;
				opacity: 1;
				box-shadow: 0rpx 8rpx 50rpx 5rpx rgba(205, 205, 205, 0.25);

				>.gift-active {
					padding: 16rpx 14rpx 16rpx 16rpx;
					box-sizing: border-box;
					position: relative;

					.active-content {
						height: 100%;
						border-radius: 10rpx;
						box-sizing: border-box;
						border: 2rpx dashed rgba(184, 0, 0, 0.4);
						padding: 24rpx 24rpx 26rpx 24rpx;

						.content-gift {
							width: 100%;
							height: 16rpx;
							background: #f0f0f0;
							border-radius: 24rpx;
							box-shadow: inset 0px 4rpx 8rpx 2rpx rgba(0, 0, 0, 0.04);
							position: relative;
							margin-bottom: 58rpx;

							.gift-one {
								position: absolute;
								top: -30rpx;
								.gift-img {
									width: 60rpx;
									height: 70rpx;
								}
							}

							.gift-two {
								position: absolute;
								left: 92%;
								top: -40rpx;
							}

							.progress-bar {
								width: 60%;
								height: 16rpx;
								background: linear-gradient(90deg, #ffc24d 0%, #ff8039 100%);
								box-shadow: inset 0px 4rpx 8rpx 2rpx rgba(255, 245, 159, 0.6);
								border-radius: 24rpx;
							}
						}

						.content-result {
							margin: 0px auto;
							font-weight: 400;
							color: rgba(51, 51, 51, 0.9);
							line-height: 44rpx;
							text-align: center;

							&>span {
								color: #fe643f;
								opacity: 0.9;
							}
						}
					}
				}
			}
		}

		.activity-invalid {
			& > .gift-c-li {
				height: 236rpx; //活动过期 332 236

				.gift-active {
					.active-content {
						padding: 70rpx 24rpx 24rpx 24rpx !important;
					}
				}
			}
		}

		.header-info {
			display: flex;
			height: 300rpx;
			padding: 42rpx 0 0 32rpx;
			box-sizing: border-box;
			background: url("~@/static/images/header-back.png") no-repeat;
			background-size: 100% 100%;
			border-radius: 0 0 24rpx 24rpx;

			.h-img {
				width: 96rpx;
				height: 96rpx;
				background: rgba(255, 255, 255, 0.8);
				margin-right: 26rpx;
			}

			.h-name {
				flex: 1;

				.name-prize {
					display: flex;
					justify-content: space-between;
					margin-bottom: 14rpx;

					.name {
						font-size: 28rpx;
						font-weight: 600;
						color: #ffffff;
						line-height: 32rpx;
						margin-top: 5rpx;
					}

					.my-prize {
						font-weight: 500;
						color: #FF8D4D;
						height: 48rpx;
						background: #FFECE4;
						box-shadow: 4rpx 4rpx 32rpx 2rpx rgba(255, 105, 64, 0.3);
						border: 2rpx solid #FF9C65;
						padding: 0px 16rpx 0 24rpx;
						display: flex;
						align-items: center;
						border-radius: 40rpx 0 0 40rpx;

						.prize {
							margin-right: 8rpx;
						}
					}
				}

				.pm {
					font-weight: 400;
					color: #ffffff;
					display: flex;
					justify-content: space-between;
					padding-right: 32rpx;
				}
			}
		}

	}

	.header-bottom {
		margin-bottom: 154rpx; //282
	}
</style>
