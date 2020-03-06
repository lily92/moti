<template>
	<view>
		<view class="padding-lf30  bgf9">
			<view class="banner">
				<image src="../../static/images/suit-banner.jpg" mode="widthFix" class="w100"></image>
			</view>
			<view class="gift flex flex-al-center flex-just-between ">
				<view class="gift-img">
					<image src="../../static/images/gift.png" mode="widthFix" class="w100"></image>
				</view>
				<view class="gift-con">
					<view class=" colorr fon28">
						运营大礼包
					</view>
					<view class="">
						10套经典魔塑+米兰魔姿产品
					</view>
				</view>
				<view class="gift-btn text-center colorf fon28">
					领取
				</view>
			</view>
		</view>

		<view class="padding-lf30">
			<view class="order-item flex flex-just-between flex-al-center" v-for="(item,index) in suitList" :key="index">

				<view class="order-img">
					<image :src="item.picLink" mode="widthFix" class="w100"></image>
				</view>
				<view class="order-con">
					<view class=" fon28 name">
						{{item.name}}
					</view>
					<view class="">
						<text class="fon32 color-org">￥{{item.price}}</text>
						<text class="line-through color9">￥{{item.priceYj}}</text>
					</view>
					<view class="color9 line2  product-desc">
						{{item.productDesc}}
					</view>
				</view>
				<view class="suit-btn">
					<image src="../../static/images/suit-btn.png" mode="widthFix" class="w100"></image>
				</view>
			</view>
		</view>
		<view class="cat-btn colorf">
			+ 1035
		</view>
		
		<view class="masters flex flex-al-center flex-just-center"  v-if="isAgent">
			<view class="box ">
				<view class="btn-close">
					关闭按钮
				</view>
				<view class=" text-center">
					<image src="../../static/images/suit-tip-img.png" mode="widthFix" class="w286"></image>
					<view class="line-h2">
						<view class="fon32 padding-t30">
							很抱歉，您还不是代理商
						</view>
						<view class="fon32">
							无法购买套装
						</view>
					</view>
					<view class="btns btns-active  fon32 colorf text-center suit-btns">
						成为代理商
					</view>
				
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	import tuiLoadmore from "@/components/loadmore/loadmore"
	import tuiNomore from "@/components/nomore/nomore"
	export default {
		components: {
			tuiLoadmore,
			tuiNomore
		},
		data() {
			return {
				pageIndex: 0,
				loadding: false,
				pullUpOn: true,
				isAgent:false,
				suitList: [{
						"id": 12,
						"picLink": "../../static/images/icon-fenlei.jpg",
						"price": "158",
						"priceYj": "1058",
						"productDesc": "1身材管理魔体仪身材管理魔体仪体仪魔体仪魔体仪...",
						"dladd_id": 100,
						"name": "身材管理魔体仪"
					},
					{
						"id": 122,
						"picLink": "../../static/images/icon-fenlei.jpg",
						"price": "158",
						"priceYj": "1058",
						"productDesc": "2身材管理魔体仪身材管理魔体仪体仪魔体仪魔体仪...",
						"dladd_id": 102,
						"name": "身材管理魔体仪"
					}, {
						"id": 1233,
						"picLink": "../../static/images/icon-fenlei.jpg",
						"price": "158",
						"priceYj": "1058",
						"productDesc": "3身材管理魔体仪身材管理魔体仪体仪魔体仪魔体仪...",
						"dladd_id": 100,
						"name": "身材管理魔体仪"
					},
					{
						"id": 12323,
						"picLink": "../../static/images/icon-fenlei.jpg",
						"price": "158",
						"priceYj": "1058",
						"productDesc": "4身材管理魔体仪身材管理魔体仪体仪魔体仪魔体仪...",
						"dladd_id": 102,
						"name": "身材管理魔体仪"
					}
				],
				loadData:[{
						"id": 12,
						"picLink": "../../static/images/icon-fenlei.jpg",
						"price": "158",
						"priceYj": "1058",
						"productDesc": "5身材管理魔体仪身材管理魔体仪体仪魔体仪魔体仪...",
						"dladd_id": 100,
						"name": "身材管理魔体仪"
					},
					{
						"id": 122,
						"picLink": "../../static/images/icon-fenlei.jpg",
						"price": "158",
						"priceYj": "1058",
						"productDesc": "6身材管理魔体仪身材管理魔体仪体仪魔体仪魔体仪...",
						"dladd_id": 102,
						"name": "6身材管理魔体仪"
					}]
			};
		},
		mounted() {
			// this.getData()
		},
		methods: {
			getData: function() {
				var _this = this
				if (_this.loadding == true) {
					return false
				}
				_this.loadding = true;
				var param = {
					page: _this.pageIndex + 1,
				}
				_this.tui.request('/mine/suitList', param).then(function(data) {
					_this.loadding = false;
					if (data.stat == 1) {

						_this.pageIndex = data.data.curpage
						_this.pullUpOn = data.data.more;
						_this.suitList = _this.suitList ? _this.suitList.concat(data.data.list) : data.data.list;
					}
				});
			},
		},
		/**
		 * 页面相关事件处理函数--监听用户下拉动作
		 */
		onPullDownRefresh: function() {
			//延时为了看效果
			setTimeout(() => {
				this.suitList = this.loadData;
				this.pageIndex = 1;
				this.pullUpOn = true;
				this.loadding = false;
				uni.stopPullDownRefresh();
				this.tui.toast("刷新成功")
			}, 200)
		},
		/**
		 * 页面上拉触底事件的处理函数
		 */
		onReachBottom: function() {
			if (!this.pullUpOn) return;
			this.loadding = true;
			// console.log(this.pageIndex, "xxx")
			this.getData()
			if (this.pageIndex == 3) {
				this.loadding = false;
				this.pullUpOn = false
			} else {
				this.suitList = this.suitList.concat(this.loadData);
				this.pageIndex = this.pageIndex + 1;
				this.loadding = false
			}
		}

	}
</script>

<style lang="scss" scoped>
	.banner {
		border-radius: 20rpx 20rpx 0 0;
	}

	.gift {
		padding: 30rpx 0;
	}

	.gift-btn {
		width: 110rpx;
		height: 80rpx;
		background-color: #d91c1c;
		border-radius: 20rpx;
		line-height: 80rpx;
	}

	.gift-img {
		width: 72rpx;
	}

	.gift-con {
		width: calc(100% - 220rpx);
	}

	.order-item {
		width: 100%;
		background-color: #ffffff;
		border-radius: 20rpx;
		padding:25rpx 0;
	}

	.order-img {
		width: 178rpx;
		border-radius: 5rpx;
	}

	.order-con {
		width: 400rpx
	}

	.suit-btn {
		width: 72rpx;
	}

	.cat-btn {
		height: 63rpx;
		background-color: #000000;
		box-shadow: 0rpx 9rpx 9rpx 0rpx rgba(247, 193, 129, 0.11);
		border-radius: 32rpx;
		display: inline-block;
		background: url(~@/static/images/gouwucheman.png) no-repeat 10rpx center #000;
		background-size: 34rpx;
		padding: 0 10rpx 0 54rpx;
		line-height: 63rpx;
		position: fixed;
		right: 40rpx;
		bottom: 100rpx;
	}
	.masters{ position: fixed; left:0; bottom: 0; right:0;  top:0; z-index: 99;  background: rgba($color: #000000, $alpha: .6);}
	.box {
		width: 630rpx;
		height: 650rpx;
		background-color: #ffffff;
		border-radius: 20rpx;
		position: relative;
		padding: 60rpx;
	}
	.btn-close{ width: 53rpx; height:53rpx; background: url(~@/static/images/suit-btn.png) no-repeat center;  background-size: contain;  position: absolute; top:-53rpx; right:30rpx; font-size: 0;}
	.w286{ width: 286rpx;}
	.line-h2{ line-height: 2;}
	.suit-btns{ line-height: 80rpx; margin-top:20rpx;}
</style>
