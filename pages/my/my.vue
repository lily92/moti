<template>
	<view>
		<uni-nav-bar color="#ffffff" background-color="#007AFF" :status-bar="true" title="我的" fixed="ture"  />
		<view class="top-bg positionr">
			<image src="../../static/images/top-bg11.jpg" mode=" width" class="w100"></image>
			<view class="flex flex-just-between flex-al-center positionb main">
				<navigator url="../personalData/personalData" class="my-icon">
					<image src="../../static/images/icon-fenlei.jpg" mode="widthFix" class="w100"></image>
				</navigator>
				<navigator url="../personalData/personalData"  class="my-con">
					<view class="">
						<text class="colorf fon32">尼古拉斯赵四</text>
						<text class="my-desc ">合伙人</text>
					</view>
					<view class=" colorf">
						ID :158461
					</view>
				</navigator>
				<navigator class="my-info" url="../myInfo/myInfo">
					<view class="info-icon positionr">
						<view class="info-read">
							16
						</view>
					</view>
				</navigator>
			</view>
		</view>

		<view class="padding-lf30">
			<!-- item -->
			<view class="index-item flex flex-just-between ">
				<view v-for="(item,index) in priceList" :key="index" class="item">
					<view class="fon42 colorf top text-center">
						{{item.money}}
					</view>
					<view class="bottom  text-center colorf">
						<view class="colorf yuan ">
							元
						</view>
						<view class="fon32">
							{{item.title}}
						</view>

					</view>
				</view>
			</view>
			<!-- end item -->
			
			<!-- 个人中心 -->
			<view class="personal">
				<view class="text-center fon32">
					个人中心
				</view>
				<view class="navlist flex ">
					<navigator :url="item.link"  v-for="(item,index) in navList" :key="index" class="nav-item">
						<image :src="item.icon" mode="widthFix" class="icon"></image>
						<view  class="title">{{item.title}}</view>
					</navigator>
				</view>
			</view>
			<navigator url=""></navigator>
			<!-- end 个人中心 -->
		</view>
		<navigator url=""></navigator>
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
				priceList: [{
						"money": "1230",
						"title": "开发奖励"
					},
					{
						"money": "1230",
						"title": "其他奖励"
					},
					{
						"money": "1230",
						"title": "返单奖励"
					}
				],
				navList:[
					{
						"icon":"../../static/images/my/my-icon1.png",
						"title":"我要下单",
						"link":"../buyingSuits/buyingSuits"
					},	{
						"icon":"../../static/images/my/my-icon2.png",
						"title":"我的订单（会员）",
						"link":"../menberOrder/menberOrder"
					},	{
						"icon":"../../static/images/my/my-icon3.png",
						"title":"我的订单（个人）",
						"link":"../myOrder/myOrder"
					},	{
						"icon":"../../static/images/my/my-icon4.png",
						"title":"会员订单",
						"link":"../menberOrder/menberOrder"
					},	{
						"icon":"../../static/images/my/my-icon5.png",
						"title":"我的会员",
						"link":"../myTeam/myTeam"
					},	{
						"icon":"../../static/images/my/my-icon6.png",
						"title":"我的账户",
						"link":"../myAccount/myAccount"
					},	{
						"icon":"../../static/images/my/my-icon7.png",
						"title":"收货地址",
						"link":"../address/selectAdress"
					},	{
						"icon":"../../static/images/my/my-icon8.png",
						"title":"微信客服",
						"link":"../bindWechat/bindWechat"
					},	{
						"icon":"../../static/images/my/my-icon9.png",
						"title":"邀请码",
						"link":"../recommDcode/recommDcode"
					},{
						"icon":"../../static/images/my/my-icon10.png",
						"title":"推荐榜",
						"link":"../rankingList/rankingList"
					},{
						"icon":"../../static/images/my/my-icon11.png",
						"title":"返单榜",
						"link":"../returnBonus/returnBonus"
					},
				]
			};
		}
	}
</script>

<style lang="scss" scoped>
	.top-bg {
		width: 100%;
		height: 301rpx;
		// background: url(~@/static/images/top-bg1.jpg) no-repeat center #000;
		background-size: 100%;
		position: relative;
		border-radius: 0 0 0 60rpx;
		 overflow: hidden;
		
	}
	.main{ left:0; top:0; width: 100%; height:100%;padding: 60rpx 30rpx; box-sizing: border-box;}

	.my-icon {
		width: 120rpx;
		height: 120rpx;
		border-radius: 20rpx;
		background: #F9F9F9;
		border: solid 2rpx #fde1b7;
		overflow: hidden;
	}

	.info-icon {
		width: 26rpx;
		height: 26rpx;
		background: url(~@/static/images/my/icon-info.png) no-repeat center;
		background-size: 26rpx;
	}

	.info-read {
		width: 35rpx;
		height: 35rpx;
		border-radius: 50%;
		background: #f9c276;
		color: #fff;
		text-align: center;
		line-height: 30rpx;
		transform: scale(0.7);
		right: -20rpx;
		top: -10px;
		position: absolute;
	}

	.my-con {
		width: calc(100% - 200rpx);
	}

	.my-desc {
		margin-left: 10rpx;
		min-width: 85rpx;
		display: inline-block;
		line-height: 30rpx;
		background-image: linear-gradient(-18deg,
			#fecc87 0%,
			#fde1b7 100%),
			linear-gradient(#fde1b7,
			#fde1b7);
		background-blend-mode: normal,
			normal;
		border-radius: 15rpx 0rpx 15rpx 15rpx;
		color: #c27b19;
		text-align: center;
	}

	.index-item {
		margin-top:-50rpx;
		position: relative;

		.item {
			width: 210rpx;
			height: 258rpx;
			border-radius: 20rpx;
			overflow: hidden;
			box-shadow: 0rpx 2rpx 16rpx 0rpx 
					rgba(0, 0, 0, 0.07);
		}

		.item:first-child {
			background: #2c2c2c;
		}

		.item:nth-child(2) {
			background: #f9c276;
		}

		.item:nth-child(3) {
			background: #fff;
		}

		.top {
			padding: 48rpx 20rpx 30rpx;
			height: 130rpx;
			box-sizing: border-box;
		}

		.bottom {
			height: 130rpx;
			position: relative;
			padding-top: 40rpx;
		}

		.yuan {
			position: absolute;
			top: -20rpx;
			left: 0;
			width: 100%;
		}

		.item:first-child .bottom {
			background-color: #383838;
			border-radius: 65rpx 0rpx 20rpx 20rpx;
		}
		.item:nth-child(2) .bottom {
			background-color: #f8b568;
			 border-radius: 0 0 20rpx 20rpx;
		}

		.item:nth-child(3) .colorf {
			color: #dba05c !important;
		}
		.item:nth-child(3) .top {
			background: #f3f3f3;
			 border-radius: 0 0 40rpx 0;
		}
		
	}
	.personal{ padding: 60rpx 0; text-align: center;
	 .icon{ width: 70rpx; height:70rpx; margin: 0 auto; display:block}
	 .nav-item{ width: 33.33%; margin-top: 30rpx;}
	 .title{ padding: 20rpx 0 0 0;}
	}
</style>
