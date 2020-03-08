<template>
	<view class="container">

		<scroll-view scroll-y scroll-with-animation class="tab-view" :scroll-top="scrollTop" :style="{height:height+'px',top:top+'px'}">
			<view v-for="(item,index) in tabbar" :key="index" class="tab-bar-item" :class="[currentTab==index ? 'active' : '']"
			 :data-current="index" @tap.stop="swichNav">
				<text>{{item}}</text>
			</view>
		</scroll-view>
		<block v-for="(item,index) in tabbar" :key="index">
			<scroll-view scroll-y class="right-box" :style="{height:height+'px',top:top+'px'}" v-if="currentTab==index">
				<view class="page-view">
					<view class="class-box">
						<view class="class-item">
							<view class="class-name color0">{{item}}</view>
							<view class="g-container">
								<view v-for="(item,index) in productLists" :key="index"  class="g-box" @tap.stop="productList" :data-id="item.id">
									<image :src="item.img" class="g-image" />
									<view class="g-title">
										<view class="fon28 line2">
											{{item.productName}}
										</view>
										<view class="fon32 color-org">
											￥{{item.price}}
										</view>
									</view>
								</view>
							</view>
						</view>
					</view>
				</view>
				<!--内容部分 end 自定义可删除-->
			</scroll-view>
		</block>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				tabbar: ["经典魔体", "进口超市", "国际名牌", "奢侈品", "海囤全球", "男装", "女装", "男鞋", "女鞋", "钟表珠宝", "手机数码", "电脑办公", "家用电器", "玩具乐器",
					"运动户外", "宠物生活", "特产馆"
				],
				productLists:[
					{
						'id':1002,
						'img':"../../static/images/icon-fenlei.jpg",
						'productName':'产品名称',
						'price':'126'
					},{
						'id':1003,
						'img':"../../static/images/icon-fenlei.jpg",
						'productName':'产品名称',
						'price':'126'
					},{
						'id':1004,
						'img':"../../static/images/icon-fenlei.jpg",
						'productName':'产品名称',
						'price':'126'
					},{
						'id':1005,
						'img':"../../static/images/icon-fenlei.jpg",
						'productName':'产品名称',
						'price':'126'
					}
				],
				height:0, //scroll-view高度
				top: 0,
				currentTab: 0, //预设当前项的值
				scrollTop: 0 //tab标题的滚动条位置
			}
		},
		onLoad: function(options) {
			setTimeout(() => {
				uni.getSystemInfo({
					success: (res) => {
						let header = 20;
						let top = 0;
						//#ifdef H5
						top = 44;
						//#endif
						this.height = res.windowHeight - uni.upx2px(header)
						this.top = top + uni.upx2px(header)
					}
				});
			}, 50)
		},
		methods: {
			// 点击标题切换当前页时改变样式
			swichNav: function(e) {
				let cur = e.currentTarget.dataset.current;
				if (this.currentTab == cur) {
					return false;
				} else {
					this.currentTab = cur;
					this.checkCor();
				}
			},
			//判断当前滚动超过一屏时，设置tab标题滚动条。
			checkCor: function() {
				let that = this;
				//这里计算按照实际情况进行修改，动态数据要进行动态分析
				//思路：窗体高度/单个分类高度 200rpx 转px计算 =>得到一屏幕所显示的个数，结合后台传回分类总数进行计算
				//数据很多可以多次if判断然后进行滚动距离计算即可
				if (that.currentTab > 7) {
					that.scrollTop = 500
				} else {
					that.scrollTop = 0
				}
			},
			detail(e) {
				uni.navigateTo({
					url: '../extend-view/productDetail/productDetail'
				})
			},
			productList(e) {
				let id = e.currentTarget.dataset.id;
				uni.navigateTo({
					url: '../productDetail/productDetail?id='+id
				})
			},
			search: function() {
				uni.navigateTo({
					url: '../extend-view/news-search/news-search'
				})
			}
		}
	}
</script>

<style>
	page {
		background: #F9F9F9;
	}

	/* 左侧导航布局 start*/

	/* 隐藏scroll-view滚动条*/

	::-webkit-scrollbar {
		width: 0;
		height: 0;
		color: transparent;
	}


	.tab-view {
		/* height: 100%; */
		min-height: 85vh;
		width: 200upx;
		position: fixed;
		left: 0;
		z-index: 10;
		padding-left: 10rpx;
	}

	.tab-bar-item {
		width: 164rpx;
		height:85rpx;
		box-sizing: border-box;
		display: flex;
		align-items: center;
		justify-content: center;
		font-size: 28rpx;
		color: #444;
		font-weight: 400;
		margin-bottom: 10rpx;
	}

	.active {
		position: relative;
		color: #000;
		font-size: 30rpx;
		/* font-weight: 600; */
		background: url(~@/static/images/icon-select.png) no-repeat center;
		background-size: 100%;
	}



	/* 左侧导航布局 end*/

	.right-box {
		width: 100%;
		position: fixed;
		padding-left: 220rpx;
		box-sizing: border-box;
		left: 0;
	}

	.page-view {
		width: 100%;
		overflow: hidden;
		padding-top: 20rpx;
		padding-right: 20rpx;
		box-sizing: border-box;
		padding-bottom: env(safe-area-inset-bottom);
	}

	.swiper {
		width: 100%;
		height: 220rpx;
		border-radius: 12rpx;
		overflow: hidden;
		transform: translateZ(0);
	}

	/* #ifdef APP-PLUS || MP */
	.swiper .wx-swiper-dot {
		width: 8rpx;
		height: 8rpx;
		display: inline-flex;
		background: none;
		justify-content: space-between;
	}

	.swiper .wx-swiper-dot::before {
		content: '';
		flex-grow: 1;
		background: rgba(255, 255, 255, 0.8);
		border-radius: 16rpx;
		overflow: hidden;
	}

	.swiper .wx-swiper-dot-active::before {
		background: #fff;
	}

	.swiper .wx-swiper-dot.wx-swiper-dot-active {
		width: 16rpx;
	}

	/* #endif */

	/* #ifdef H5 */
	>>>.swiper .uni-swiper-dot {
		width: 8rpx;
		height: 8rpx;
		display: inline-flex;
		background: none;
		justify-content: space-between;
	}

	>>>.swiper .uni-swiper-dot::before {
		content: '';
		flex-grow: 1;
		background: rgba(255, 255, 255, 0.8);
		border-radius: 16rpx;
		overflow: hidden;
	}

	>>>.swiper .uni-swiper-dot-active::before {
		background: #fff;
	}

	>>>.swiper .uni-swiper-dot.uni-swiper-dot-active {
		width: 16rpx;
	}
  
	/* #endif */



	.class-box {
		padding-top: 0;
	}

	.class-item {
		background: #fff;
		width: 100%;
		box-sizing: border-box;
		padding: 20rpx;
		margin-bottom: 10rpx;
		border-radius: 12rpx;
	}

	.class-name {
		font-size: 26rpx;
	}

	.g-container {
		/* padding-top: 20upx; */
		display: flex;
		display: -webkit-flex;
		justify-content: flex-start;
		flex-direction: row;
		flex-wrap: wrap;
	}

	.g-box {
		width: 100%;
		padding-top: 40rpx;
		display: flex;
		align-items: center;
	}

	.g-image {
		width: 140rpx;
		height: 140rpx;
		background: #F7F7F7;
		border-radius: 10rpx;
		margin-right: 20rpx;
		flex-shrink: 0;
	}

	.g-title {
		font-size: 22rpx;
	}
	.right-box{min-height: 85vh;}
</style>
