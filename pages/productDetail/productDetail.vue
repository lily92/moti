<template>
	<view>
		<view class="product-img">
			<image src="../../static/images/product-detail-img.jpg" mode="widthFix" class="w100"></image>
		</view>
		<view class="product-con positionr">
			<!-- 加入购物车按钮，分享按钮 -->
			<view class=" flex positionb btn-groups">
				<view class="btn-cart">

				</view>
				<view class="btn-share">

				</view>
			</view>
			<!-- end 加入购物车按钮，分享按钮 -->
			<view class=" ">
				<text class="color-org fon42">￥158</text>
				<text class="color-org margin-l30">免运费</text>
			</view>
			<view class="fon32 product-name">
				身材管理魔体仪
			</view>
			<view class="product-desc color9 line2 margin-b20">
				身材管理魔体仪身材管理魔体仪体仪魔体仪魔体仪魔体仪仪魔体仪
				魔仪魔体仪魔仪魔体仪魔
			</view>

			<!--star  选择规格 -->
			<view class="flex flex-al-center flex-just-between margin-b20">
				<view class="guige-btn">
				</view>
				<view class="">
					<view class="fon28">
						规格
					</view>
					<view class=" color9 borderb">
						S码 / 黑色 / 升级版
					</view>
				</view>
				<view class="more" @tap="showGuigeFun(true)">
					<view class="more-btn">

					</view>
				</view>
			</view>
			<!--end   选择规格 -->
			<!--star  地址 -->
			<view class="flex flex-al-center flex-just-between">
				<view class="guige-btn">
				</view>
				<view class="">
					<view class="fon28">
						地址
					</view>
					<view class=" color9 borderb">
						广州市白云区凯云商务中心暗示设计
					</view>
				</view>
				<view class="more">
					<navigator class="more-btn" url="../address/selectAdress">

					</navigator>
				</view>
			</view>
			<!--end   地址 -->

			<!--star 商品详情 -->
			<view class="product-detail">
				<view class="fon32  text-center  positionr title">
					<view class="title-name positionr">
						商品详情
					</view>
				</view>
				<view class="">
					<image src="../../static/images/detail-img2.jpg" mode="widthFix" class="w100"></image>
				</view>
			</view>
			<!-- end 商品详情 -->
		</view>
		<view class="btn-buy-line flex flex-just-between">
			<view class="b-btn fon28 colorf text-center">
				加入购物车
			</view>
			<view class="b-btn-1 fon28 colorf text-center">
				立即购买
			</view>
		</view>

		<!-- 商品选择规格 -->
		<view class="tui-mask" v-if="showGuige || showSize">

		</view>
		<view class="product-guige bgf" :class="showGuige?'active':''">

			<view class="positionr">
				<view class="btn-close positionb " @tap="showGuigeFun(false)">

				</view>
				<view class="fon32 text-center ">
					选择规格
				</view>
				<view class="flex flex-just-between padding-t30">
					<view class="pro-imgs">
						<image src="../../static/images/icon-fenlei.jpg" mode="widthFix" class="w100"></image>
					</view>
					<view class="pro-cons flex">
						<view class="fon28 w100 name">
							商品名称名称美年广场
						</view>
						<view class="w100">
							编号：1065789
						</view>
						<view class="w100 color-org">
							（注：最低购买5套，最高按照5的倍数递增）
						</view>
					</view>

				</view>

				<!-- list -->
				<view class="padding-t30">
					<view class="flex flex-just-between">
						<view class="prod fon28">
							商品
						</view>
						<view class="size fon28  ">
							尺寸
						</view>
						<view class="number fon28  tui-text-right">
							数量
						</view>
					</view>

					<view v-for="(item,index) in guigeList" :key="index" class="flex flex-just-between guige-list flex-al-center">
						<view class="prod fon28">
							{{item.name}}
						</view>
						<view class="size fon28  ">
							<picker @change="bindPickerChange" :data-index='index' :value="item.selectIndex" :range="item.size">
								<view class="uni-input">{{item.size[item.selectIndex]}}</view>
							</picker>
						</view>
						<view class="number fon28  tui-text-right">
							<tui-numberbox :value="item.number" :min="0" :max="max" :index="index" @change="change" :iconSize='15' :bgcolor='bgf'
							 :height='72' :color="color" :borders='borders' :step="5"></tui-numberbox>
						</view>
					</view>
				</view>

			</view>
		</view>

		<view class="product-guige bgf active"  v-if="showSize">
			<view class="positionr">
				<view class="btn-close positionb " @tap="showGuigeFun(false)">

				</view>
				<view class="fon32 text-center ">
					推荐尺码
				</view>
				
				<view class="padding-t30">
					<input type="text" value=""  placeholder="身高（必填）" class="re-txt"/>
					<input type="text" value=""  placeholder="胸围（必填）" class="re-txt"/>
					<input type="text" value="" placeholder="腰围（必填）" class="re-txt" />
					<view class="re-txt flex flex-just-between flex-al-center">
						<input type="text" value="推荐尺码为：82"  class="fon24" />
						<view class="color-org">
							重新填写
						</view>
					</view>
				</view>
				<view class="padding-t30">
					<view class=" fon28">
						尺码参考
					</view>
					<view class="">
						（因测量方式不同，个人穿着习惯，建议结合尺码双重选择额）
					</view>
					<view class="padding-t30">
						<image src="../../static/images/re-img.jpg" mode="widthFix" class="w100"></image>
					</view>
				</view>
			</view>
		</view>

		<!-- end 商品规格 -->
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
				borders: "borders",
				showGuige: false,
				showSize:false,
				guigeList: [{
					"name": "商品名称",
					"selectIndex": 0,
					"size": ['36B', '35B', '36C', '38B'],
					"number": 0
				}, {
					"name": "2商品名称",
					"selectIndex": 1,
					"size": ['36B', '35B', '36C', '38B'],
					"number": 0
				}, {
					"name": "3商品名称",
					"selectIndex": 2,
					"size": ['36B', '35B', '36C', '38B'],
					"number": 0
				}, ]
			};
		},
		components: {
			tuiNumberbox,
		},
		methods: {
			showGuigeFun(isshow) {
				this.showGuige = isshow
			},
			change: function(e) {
				console.log(e)
				// this.number = e.value
				console.log(this.guigeList[e.index].number);
				this.guigeList[e.index].number = e.value;
			},
			bindPickerChange: function(e) {

				console.log('picker发送选择改变，携带值为', e.target.value)
				console.log(e.target.dataset.index)
				let parentIndex = e.target.dataset.index
				this.selectIndex = e.target.value
				this.guigeList[parentIndex].selectIndex = e.target.value
			},
		}
	}
</script>

<style lang="scss" scoped>
	.product-con {
		padding: 50rpx 30rpx;
		border-radius: 30rpx;
		margin-top: -60rpx;
		position: relative;
		z-index: 2;
		background: #fff;
	}

	.product-name {
		padding: 40rpx 0 30rpx
	}

	.product-desc {
		margin-bottom: 30rpx;
	}

	.guige-btn {
		width: 38rpx;
		height: 38rpx;
		background: url(~@/static/images/icon-right.png) no-repeat center;
		background-size: 38rpx;
	}

	.borderb {
		border-bottom: 1px solid #e4e4e4;
		width: 610rpx;
		padding: 10rpx 0;
	}

	.more {
		padding: 10rpx 10rpx;
	}

	.more-btn {
		width: 4rpx;
		height: 19rpx;
		background: url(~@/static/images/common/icon-more.png) no-repeat center;
		background-size: 4rpx 19rpx;
	}

	.product-detail {
		padding-top: 60rpx;
		padding-bottom: 150rpx;
	}

	.title::before {
		height: 8rpx;
		width: 147rpx;
		background: #da9e5a;
		position: absolute;
		left: 50%;
		bottom: 4rpx;
		transform: translateX(-50%);
		z-index: 1;
		content: ''
	}

	.title-name {
		z-index: 3;
		margin-bottom: 30rpx;
	}

	.btn-buy-line {
		width: 100%;

		background-color: #ffffff;
		box-shadow: 0rpx -10rpx 25rpx 0rpx rgba(221, 164, 97, 0.13);
		position: fixed;
		bottom: 0;
		left: 0;
		z-index: 99;
		padding: 20rpx 30rpx;
	}

	.b-btn {
		width: 331rpx;
		height: 80rpx;
		line-height: 80rpx;
		background-color: #000000;
		border-radius: 20rpx;
	}

	.b-btn-1 {
		width: 331rpx;
		height: 80rpx;
		line-height: 80rpx;
		background-color: #dda461;
		border-radius: 20rpx;
	}

	.btn-cart {
		width: 104rpx;
		height: 104rpx;
		background: url(~@/static/images/cart-btn.png) no-repeat center;
		background-size: 104rpx;
	}

	.btn-share {
		width: 104rpx;
		height: 104rpx;
		background: url(~@/static/images/share-icon.png) no-repeat center;
		background-size: 104rpx;
		margin-left: 20rpx;
	}

	.btn-groups {
		right: 20rpx;
		top: -50rpx
	}

	.product-guige {
		padding: 30rpx;
		position: fixed;
		bottom: -100%;
		width: 100%;
		z-index: 98;
		background: #fff;
		transition: .3s linear all;
	}

	.product-guige.active {
		bottom: 120rpx;
	}

	.pro-imgs {
		width: 142rpx;
	}

	.pro-cons {
		width: 520rpx;
		padding: 10rpx 0;
	}

	.number {
		width: 180rpx;
		text-align: right;
	}

	.size {
		width: 80rpx;
	}

	.prod {
		width: calc(100% - 350rpx);
	}

	.guige-list {
		padding: 24rpx 0;
	}

	.tui-numberbox {
		width: 100%;
		border: 1px solid #e4e4e4;
		border-radius: 10rpx;
	}


	.uni-input {
		background: url(~@/static/images/icon-arrow.png) no-repeat right center;
		background-size: 14rpx 8rpx;
		padding-right: 15rpx;
	}

	.btn-close {
		width: 53rpx;
		height: 53rpx;
		background: url(~@/static/images/suit-btn.png) no-repeat center;
		background-size: 53rpx;
		right: 10rpx;
		top: -83rpx
	}

	.tui-mask {
		background: rgba($color: #000000, $alpha: 0.6);
		position: fixed;
		left: 0;
		top: 0;
		bottom: 0;
		right: 0;
		z-index: 8;
	}
	.re-txt {
		width: 690rpx;
		height: 71rpx;
		background-color: #f9f9f9;
		border-radius: 20rpx;
		margin-bottom: 15rpx;
		padding: 0 30rpx;
		line-height: 71rpx;
		font-size: 24rpx;
	}
</style>
