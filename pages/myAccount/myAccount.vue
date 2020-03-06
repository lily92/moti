<template>
	<view>
		<view class="padding-lf30 padding-t30">
			<view class="">
				<view class="keti fon26  positionr">
					<view class="">
						我的奖励
					</view>
					<view class="fon60 keti-fon">
						￥1000
					</view>
					<view class="tixain-btn positionb colorf  text-center">
						提现
					</view>
				</view>
			</view>
		
		    <view v-for="(item,index) in list" :key="index" class="item flex flex-al-center flex-just-between">
		    	<view class="">
		    		<view class=" color9 title">
		    			{{item.title}}
		    		</view>
					<view class="fon42 color0">
						{{item.money}}
					</view>
		    	</view>
				<view class="iconw">
					<image :src="item.icon" mode="widthFix" class="w100"></image>
				</view>
		    </view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				list:[
					{
						"title":"推荐奖励",
						"money":"189,556",
						"icon":"../../static/images/myaccount/icon1.png"
					},
					{
						"title":"团队奖励",
						"money":"189,556",
						"icon":"../../static/images/myaccount/icon2.png"
					},{
						"title":"订单奖励",
						"money":"189,556",
						"icon":"../../static/images/myaccount/icon3.png"
					}
				]
			};
		}
	}
</script>

<style lang="scss" scoped>
	page {
		background: #f9f9f9;
	}

	.keti {
		padding: 60rpx;
		background: #000;
		border-radius: 20rpx;
		color: #fff;
		margin-bottom: 30rpx;
		background: url(~@/static/images/tixain-bg.png) no-repeat center;
		background-size: 100%;
	}

	.keti-fon {
		padding: 50rpx 0 0 0;
	}

	.tixain-btn {
		width: 163rpx;
		height: 60rpx;
		background-image: linear-gradient(67deg,
			#da9e5a 0%,
			#f4d195 100%),
			linear-gradient(#fff1e0,
			#fff1e0);
		background-blend-mode: normal,
			normal;
		border-radius: 30rpx 0px 0rpx 30rpx;
		right: 0;
		top: 50%;
		transform: translateY(-50%);
		line-height: 60rpx;
	}

	.tixain-btn::before {
		content: '';
		width: 16rpx;
		height: 16rpx;
		
		 border: solid 1rpx #ffffff;
		 right:130rpx; top:50%; transform: translateY(-50%);
		 display: block;
		 position: absolute; border-radius: 50%;
	}
	.item {
		width: 690rpx;
		height: 206rpx;
		background-color: #ffffff;
		border-radius: 20rpx;
		margin-bottom: 30rpx;
		padding: 60rpx;
	}
	.iconw{ width:60rpx;}
	.title{ padding: 8rpx 0;}
</style>
