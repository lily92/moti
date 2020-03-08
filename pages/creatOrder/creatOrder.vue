<template>
	<view class="padding-lf30 padding-t30">
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
			<view class="more-btn">
				<image src="../../static/images/common/icon-more.png" mode="widthFix" class="w100">
				</image>
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
				<tui-numberbox :value="number" :min="0" :max="max" :index="index" @change="change" :iconSize='15' :bgcolor='bgf' :height='72'
				 :color="color"></tui-numberbox>
			</view>
		</view>

		<view class="message">
			<view class="margin-l30">
				留言
			</view>
			<view class="message-box">
				<input type="text" value="" placeholder="请输入留言" class="w100 txt fon24" />
			</view>
		</view>

		<view class="pinzheng margin-t30">
			<view class="margin-l30">
				上传支付凭证
			</view>
			<view class="message-box shangchuan flex flex-al-center ">
				<view class="w100 text-center">
					<view class="fon42 color9">
						+
					</view>
					<view class=" color9">
						点击上传
					</view>
				</view>
			</view>
		</view>
	
	    <view class="btn-fix flex  flex-just-between flex-al-center">
	    	<view class="numbers colorf text-center flex flex-al-center">
	    		<view class="w100">
	    			<view class="">
	    				15687
	    			</view>
	    			<view class="">
	    				总计/套
	    			</view>
	    		</view>
	    	</view>
			<view class=" btns btns-tijiao btntijiao fon28 colorf">
				提交订单
			</view>
	    </view>
	</view>
</template>

<script>
	import tuiNumberbox from "@/components/numberbox/numberbox"
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
			tuiNumberbox,
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
		width: calc(100% - 130rpx);
	}

	.more-btn {
		width: 6rpx;
		margin-right: 20rpx;
	}

	.order-item {
		
		height: 239rpx;
		background-color: #ffffff;
		border-radius: 20rpx;
		margin-top: 30rpx;
		padding: 30rpx ;
	}

	.order-img {
		width: 178rpx;
		border-radius: 5rpx;
	}

	.order-con {
		width: calc(100% - 260rpx);
	}

	.list-count {
		width: 50rpx;
		border: 1px solid #eaeaea;
		border-radius: 10rpx;
		height: 176rpx
	}

	.list-content {
		width: calc(100% - 500rpx);
	}

	.count {
		line-height: 58rpx;
		color: #666
	}

	.num {
		border-top: 1px solid #eaeaea;
		border-bottom: 1px solid #eaeaea;
		color: #90A0E4
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
	.message-box.shangchuan{
		height: 240rpx;
	}

	.txt {
		border-bottom: 1px solid #e4e4e4;
		padding: 20rpx 0;
		height: 100%
	}

	.margin-l30 {
		margin-left: 30rpx;
	}
	.name{ padding: 0 0 10rpx 0;}
	.product-desc{ padding-top: 10rpx;}
	.btn-fix {
		width: 100%;
		height: 166rpx;
		background-color: #ffffff;
		box-shadow: 0rpx -10rpx 25rpx 0rpx 
			rgba(221, 164, 97, 0.13);
			position: fixed;
			bottom: 0;
			left: 0;
			z-index: 2;
			padding: 10rpx 30rpx 40rpx 30rpx;
	}
	.btntijiao {
		width:calc(100% - 200rpx);
		height: 80rpx;
		background-image: linear-gradient(67deg, 
			#da9e5a 0%, 
			#f4d195 100%), 
		linear-gradient(
			#dda461, 
			#dda461);
		background-blend-mode: normal, 
			normal;
		border-radius: 20rpx;
		text-align: center;
	}
	.numbers {
		width: 163rpx;
		height: 80rpx;
		background-color: #000000;
		border-radius: 20rpx;
	}
</style>
