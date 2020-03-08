<template>
	<view class="">
		<view class="flex flex-just-between cart-top ">
			<view class=" color9">
				（注：最低购买5套，最高按照5的倍数递增）
			</view>
			<view class=" fon26">
				完成
			</view>
		</view>
		<view class="">
			<view class="order-item flex flex-just-between flex-al-center" v-for="(item,index) in list" :key="index">
				<view>
					<checkbox :value="item.dladd_id.toString()" :checked="item.dladd_default===1" color="#dda461" />
				</view>
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
					<tui-numberbox :value="item.number" :min="0" :max="max" :index="index" @change="change" :iconSize='15' :bgcolor='bgf'
					 :height='72' :color="color" :step='step'></tui-numberbox>
				</view>
			</view>
		</view>

		<view class="btn-fix flex  flex-just-between flex-al-center">
			<view class="check-all">
				<checkbox color="#dda461" />
				<view class=" color9">
					全选
				</view>
			</view>
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
				number: 0,
				bgf: '#fff',
				index: 0,
				max: 2100,
				step: 5,
				list: [{
						"picLink": "../../static/images/icon-fenlei.jpg",
						"price": "158",
						"priceYj": "1058",
						"productDesc": "身材管理魔体仪身材管理魔体仪体仪魔体仪魔体仪...",
						"number": 10,
						"dladd_id": 100,
						"dladd_default": 1
					},
					{
						"picLink": "../../static/images/icon-fenlei.jpg",
						"price": "158",
						"priceYj": "1058",
						"productDesc": "身材管理魔体仪身材管理魔体仪体仪魔体仪魔体仪...",
						"number": 10,
						"dladd_id": 102,
						"dladd_default": 0
					}
				]
			};
		},
		components: {
			tuiNumberbox,
		},
		methods: {
			change: function(e) {
				// console.log(e)
				this.list[e.index].number = e.value
			},
		}
	}
</script>

<style lang="scss" scoped>
	.cart-top {
		border-bottom: 10rpx solid #F9F9F9;
		padding: 20rpx 30rpx;
	}

	.order-item {
		
		height: 239rpx;
		background-color: #ffffff;
		border-radius: 20rpx;
		padding: 30rpx;
	}

	.order-img {
		width: 178rpx;
		border-radius: 5rpx;
	}

	.order-con {
		width: calc(100% - 340rpx);
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

	.btn-fix {
		width: 100%;
		height: 166rpx;
		background-color: #ffffff;
		box-shadow: 0rpx -10rpx 25rpx 0rpx rgba(221, 164, 97, 0.13);
		position: fixed;
		bottom: 0;
		left: 0;
		z-index: 2;
		padding: 10rpx 30rpx 40rpx 30rpx;
	}

	.btntijiao {
		width: 330rpx;
		height: 80rpx;
		background-image: linear-gradient(67deg,
			#da9e5a 0%,
			#f4d195 100%),
			linear-gradient(#dda461,
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
		margin-left: 100rpx;
	}
	.check-all{ padding-top: 20rpx;}
</style>
