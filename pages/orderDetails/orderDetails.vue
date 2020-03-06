<template>
	<view class="padding-lf30">
		<view class="fon36 text-center order-state">
			订单已提交
		</view>
		<view class="address flex flex-al-center flex-just-between">
			<view class="address-left colorf ">
				收货地址
			</view>
			<view class="address-con">
				<view class="">
					<text>阿康先生</text>
					<text>13258646856</text>
				</view>
				<view class="color6">
					广州市白云区沮丧街机三国阿三哥甲说过暗示方
				</view>
			</view>
			
		</view>

		<view class="order-item flex flex-just-between flex-al-center">
			<view class="order-img">
				<image src="../../static/images/icon-fenlei.jpg" mode="widthFix" class="w100"></image>
			</view>
			<view class="order-con">
				<view class=" fon28 name">
					身材管理魔体仪
				</view>
				<view class="">
					<text class="fon32 color-org">￥158</text>
					<text class="line-through color9">￥1058</text>
				</view>
				<view class="color9 line2  product-desc">
					身材管理魔体仪身材管理魔体仪体
					仪魔体仪魔体仪...
				</view>
			</view>
			<view class="list-count text-center">
				x 15
			</view>
		</view>

		<view class="message">
			<view class="margin-l30">
				留言
			</view>
			<view class="message-box">
				<view placeholder="" class="w100 txt fon24">
					十几个说过暗示阿三哥我艾尔
				</view>
			</view>
		</view>
		
		
		<!-- 微信号，订单已提交的时候显示 -->
		<view class="message">
			<view class="margin-l30">
				微信号
			</view>
			<view class="message-box">
				<view placeholder="" class="w100 txt fon24 flex flex-al-center flex-just-between">
					<text>sdgjk14543</text>
					<image src="../../static/images/icon-copy.png" mode="widthFix" class="copy-icon"></image>
				</view>
			</view>
		</view>
		
		
		<!-- 订单详情 -->
		<view class="order-detail color6">
			<view class="flex flex-just-between">
				<text>订单编号</text>
				<text class="color0">20180918124523</text>
				
			</view>
			<view class="flex flex-just-between flex-al-between">
				<text>下单时间</text>
				<text class="color0">2018/09/18 12：45：23</text>
			</view>
		</view>
		
		<view class="btns btns-tijiao   text-center margin-auto fon28">
			取消订单
		</view>
	</view>
</template>

<script>
	
	export default {
		data() {
			return {
				color: '#da9e5a',
				number:0,
				bgf:'#fff',
				index:0,
				max:2100
			};
		},
		components: {
			
		},
		methods:{
			change: function(e) {
				// console.log(e)
				this.number = e.value
			},
		}
	}
</script>

<style lang="scss" scoped>
	page {
		background-color: #F9F9F9;
	}

	.address {
		width: 690rpx;
		height: 163rpx;
		background-color: #ffffff;
		border-radius: 20rpx;

	}

	.address-left {
		width: 71rpx;
		height: 163rpx;
		background-image: linear-gradient(67deg,
			#da9e5a 0%,
			#f4d195 100%),
			linear-gradient(#da9e5a,
			#da9e5a);
		background-blend-mode: normal,
			normal;
		border-radius: 10rpx 0rpx 0rpx 10rpx;
		padding: 10rpx 20rpx;
	}

	.address-con {
		width: calc(100% - 120rpx);
	}


	.order-item {
		width: 100%;
		height: 239rpx;
		background-color: #ffffff;
		border-radius: 20rpx;
		margin-top: 30rpx;
		padding: 30rpx;
	}

	.order-img {
		width: 178rpx;
		border-radius: 5rpx;
	}

	.order-con {
		width: calc(100% - 280rpx);
	}

	.list-count {
		width: 50rpx;
		
	}
	
	.txt {
		border-bottom: 1px solid #e4e4e4;
		padding: 20rpx 0;
		height: 100%
	}

	.line-through {
		text-decoration: line-through;
		margin-left: 10rpx;
	}

	.message {
		margin-top: 30rpx;
		margin-bottom: 30rpx;
	}
	
	.message-box {
		width: 100%;
		height: 143rpx;
		background-color: #ffffff;
		border-radius: 20rpx;
		margin-top: 10rpx;
		padding: 30rpx;
	}

	.margin-l30 {
		margin-left: 30rpx;
	}
	.name{ padding: 0 0 10rpx 0;}
	.product-desc{ padding-top: 10rpx;}
	.order-detail{ line-height: 1.8;}
	.copy-icon{ width: 22rpx;}
	.order-state{ padding: 60rpx 0;}
	
</style>
