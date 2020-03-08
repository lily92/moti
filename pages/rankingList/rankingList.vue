<template>
	<view class="bg-org">
		<uni-nav-bar color="#000" background-color="#007AFF" :status-bar="true" title="排名" @clickLeft="back" left-icon="arrowleft"
		 :bg='bgrank' fixed="true" />
		<view class="">
			<view>
				<image src="../../static/images/rank/2.jpg" mode="widthFix" class="w100"></image>
			</view>
			<view class="w100 text-center">
				<image src="../../static/images/rank/r-title.png" mode="widthFix" class="title"></image>
			</view>
		</view>
		<view class="box margin-auto flex">
			<view class="item">
				<image src="../../static/images/icon-fenlei.jpg" mode="widthFix" class="circle"></image>
				<view class="name colorf fon28">
					{{list[1].name}}
				</view>
				<view class="number positionb colorf">
					{{list[1].rank}}
				</view>
				<view class="size fon32 colorr text-center">
					{{list[1].number}}单
				</view>
			</view>
			<view class="item w219">
				<image src="../../static/images/icon-fenlei.jpg" mode="widthFix" class="circle"></image>
				<view class="name colorf fon28 ">
					{{list[0].name}}
				</view>
				<view class="number positionb colorf">
					{{list[0].rank}}
				</view>
				<view class="size fon32 colorr text-center">
					{{list[0].number}}单
				</view>

			</view>
			<view class="item">
				<image src="../../static/images/icon-fenlei.jpg" mode="widthFix" class="circle"></image>
				<view class="name colorf fon28 ">
					{{list[2].name}}
				</view>
				<view class="number positionb colorf">
					{{list[2].rank}}
				</view>
				<view class="size fon32 colorr text-center">
					{{list[2].number}}单
				</view>
			</view>
		</view>

		<view class="bg-org w100" style="height: 1100rpx;">
			<!-- list 前十-->
			<view class="list-top">
				<view class="bg-line">
					<view class="list-box ">
						<view v-for="(item,index) in list" :key="index" v-if="item.rank>3" class="flex flex-al-center  flex-just-between list-item">
							<view class=" fon36">
								{{item.rank}}
							</view>
							<view class=" w72">
								<image src="../../static/images/icon-fenlei.jpg" mode="widthFix" class="imgs w100"></image>
							</view>
							<view class="w250">
								<view class="name1 fon32">
									{{item.name}}
								</view>
								<view class="precent-bg">
									<view class="precent" :style="{ width: (item.precent)*100 + '%' }">
										{{item.precent}}
									</view>
								</view>
							</view>
							<view class="numbers fon36">
								{{item.number}}单
							</view>
						</view>
					</view>
				</view>
			</view>
			<!-- end list 前十 -->
		</view>
	</view>
</template>

<script>
	import uniNavBar from '@/components/uni-nav-bar/uni-nav-bar.vue'
	export default {
		components: {
			uniNavBar
		},
		data() {
			return {
				bgrank: 'bgrank',
				list: [{
					"name": "西建科",
					"rank": 1,
					"number": 1002,
					"precent": 0.9,
					"img": "../../static/images/icon-fenlei.jpg"
				}, {
					"name": "第名",
					"rank": 2,
					"number": 852,
					"precent": 0.85,
					"img": "../../static/images/icon-fenlei.jpg"
				}, {
					"name": "西红柿",
					"rank": 3,
					"number": 782,
					"precent": 0.8,
					"img": "../../static/images/icon-fenlei.jpg"
				}, {
					"name": "西建科",
					"rank": 4,
					"number": 1002,
					"precent": 0.8,
					"img": "../../static/images/icon-fenlei.jpg"
				}, {
					"name": "西建科",
					"rank": 5,
					"number": 1002,
					"precent": 0.8,
					"img": "../../static/images/icon-fenlei.jpg"
				}, {
					"name": "西建科",
					"rank": 6,
					"number": 1002,
					"precent": 0.9,
					"img": ""
				}, {
					"name": "第名",
					"rank": 7,
					"number": 852,
					"precent": 0.8,
					"img": ""
				}, {
					"name": "西建科",
					"rank": 8,
					"number": 1002,
					"precent": 0.8,
					"img": ""
				}, {
					"name": "西建科",
					"rank": 9,
					"number": 1002,
					"precent": 0.8,
					"img": ""
				}, {
					"name": "米明是",
					"rank": 10,
					"number": 1002,
					"precent": 0.8,
					"img": ""
				}]
			};
		},
		methods: {
			back() {
				uni.navigateBack({
					delta: 1
				})
			},
		}

	}
</script>

<style lang="scss" scoped>
	page {
		background: #f7b364;
	}

	// .bg-org {
	// 	background: #f7b364;
	// }

	.title {
		width: 627rpx;
		position: relative;
		z-index: 2;
		margin-top: -105rpx;
		margin-bottom: 50rpx;
	}

	.box {
		width: 690rpx;
		height: 298rpx;
		background-color: #ffffff;
		box-shadow: 8rpx 13rpx 33rpx 2rpx rgba(175, 8, 20, 0.54);
	}

	.item {
		flex: 1;
		position: relative;
	}

	.circle {
		border-radius: 50%;
		border: 1px solid #ff2a39;
		width: 109rpx;
		display: block;
		margin: 60rpx auto 0;
		position: relative;
	}

	.w219 {
		width: 220rpx;
		position: relative;
		z-index: 2;
		background: #fff;
		margin-top: -20rpx;
		border-radius: 15rpx 15rpx 0 0;
	}

	.w219::after,
	.w219::before {
		content: '';
		width: 15rpx;
		height: 213rpx;
		position: absolute;
		top: -20rpx
	}

	.w219::after {
		background: url(~@/static/images/rank/r-left.png) no-repeat center;
		background-size: 15rpx 213rpx;
		left: -15rpx;
		top: 0
	}

	.w219::before {
		background: url(~@/static/images/rank/r-right.png) no-repeat center;
		background-size: 15rpx 213rpx;
		right: -15rpx;
		top: 0
	}

	.w219 .circle {
		width: 140rpx;
	}

	.name {
		width: 192rpx;
		height: 52rpx;
		background: url(~@/static/images/rank/r-name.png) no-repeat center;
		background-size: 192rpx 52rpx;
		line-height: 40rpx;
		text-align: center;
		margin: -30rpx auto 0;
		position: relative;
		z-index: 2;
	}

	.number {
		width: 40rpx;
		height: 40rpx;
		color: #fff;
		text-align: center;
		background: #f8b96c;
		border-radius: 50%;
		top: 30rpx;
		right: 40rpx;
		line-height: 40rpx;
	}

	.size {
		padding: 20rpx 0 0 0;
	}

	.bg-line {
		width: 712rpx;
		height: 50rpx;
		background-color: #fe9c28;
		border-radius: 25rpx;
		border: solid 12rpx #ffc17a;
		margin: 30rpx auto 0;
		box-sizing: border-box;
	}

	.list-box {
		width: 659rpx;
		min-height: 873rpx;
		background-color: #ffffff;
		box-shadow: 8rpx 13rpx 33rpx 2rpx rgba(175, 8, 20, 0.54);
		border-radius: 0rpx 0rpx 20rpx 20rpx;
		margin: 10rpx auto 20rpx;
		position: relative;
		padding: 20rpx 30rpx 30rpx;
		box-sizing: border-box;
	}

	.w72 {
		width: 72rpx;
	}

	.imgs {
		border-radius: 50%;
		background: #f9f9f9;
	}

	.w250 {
		width: 250rpx;
		box-sizing: border-box;
	}

	.precent-bg {
		width: 249rpx;
		height: 16rpx;
		background-color: #ffe2c8;
		border-radius: 8rpx;
		margin: 8rpx 0;
	}

	.precent {
		width: 0;
		height: 16rpx;
		background-color: #f7b364;
		border-radius: 8rpx;
		font-size: 0;
	}

	.numbers {
		width: calc(100% - 392rpx);
	}

	.list-item {
		border-bottom: 1px solid rgba(255, 172, 178, .2);
		padding: 30rpx 0;
	}

	.bg2 {
		height: 208rpx;
		width: 100%;
		background: url(~@/static/images/rank/2.jpg) no-repeat center;
		background-size: 100%;
	}
</style>
