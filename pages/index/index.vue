<template>
	<view class="padding-lf30">
		<view class=" fon32 fonb">
			<view class=" hello">
				Hello,
			</view>
			<view class="">
				Welcome To Moti.
			</view>
		</view>
		<!--star  banner -->
		<view class="banner">
			<swiper class="swiper" :indicator-color='color' :indicator-dots="indicatorDots" :autoplay="autoplay" :interval="interval"
			 :duration="duration" :indicator-active-color='color' :loop='loop'>
				<swiper-item>
					<view class="swiper-item  positionr ">
						<image src="../../static/images/index-banner.jpg" mode="widthFix" class="w100 visible-hidden"></image>
						<video class="video" src="http://wxsnsdy.tc.qq.com/105/20210/snsdyvideodownload?filekey=30280201010421301f0201690402534804102ca905ce620b1241b726bc41dcff44e00204012882540400&bizid=1023&hy=SH&fileparam=302c020101042530230204136ffd93020457e3c4ff02024ef202031e8d7f02030f42400204045a320a0201000400"
						 poster="../../static/images/index-banner.jpg"></video>
					</view>
				</swiper-item>
				<swiper-item>
					<view class="swiper-item ">
						<image src="../../static/images/index-banner.jpg" mode="widthFix" class="w100"></image>
					</view>
				</swiper-item>
				<swiper-item>
					<view class="swiper-item">
						<image src="../../static/images/index-banner.jpg" mode="widthFix" class="w100"></image>
					</view>
				</swiper-item>
			</swiper>
		</view>
		<!--end  banner -->

		<!-- index-item1 -->
		<view class="index-item1">
			<view class=" fon32">
				MOTI魔体，源自意大利
			</view>
			<view class=" line-h2 index-desc">
				创建于1988年，品牌定位于科技速形定制专家，以新一代身材管理魔体仪和专利仪器MT5S魔雕仪，系统打造女性完美魔鬼身材，全面提升广大女性的生活品质成就更多女性优雅、自信、幸福的人生。
			</view>

			<view class="index-img flex flex-just-between">
				<view class="w330">
					<image src="../../static/images/index-img1.jpg" mode="widthFix" class="w100"></image>
				</view>
				<view class="w330">
					<image src="../../static/images/index-img2.jpg" mode="widthFix" class="w100"></image>
				</view>
				<view class="w100">
					<view class="w610 positionr">
						<image src="../../static/images/index-img3.jpg" mode="" class="w100"></image>
						<view class="positionb bgf index-about">
							2008年，魔体登陆亚太，后在香港成立意大利魔体生活（香港）有限公司，倾力打造适合中国人的魔体美学文化。
						</view>
					</view>
				</view>
			</view>
		</view>
		<!-- end index -item1 -->

		<view class="index-list">
			<view class=" hello fon36">
				爆款发售
			</view>
			<view class="list-item">
				<view v-for="(item,index) in proList" :key="index" class="flex list-items flex-just-between">
					<view class="order-img">
						<image src="../../static/images/icon-fenlei.jpg" mode="widthFix" class=""></image>
					</view>
					<view class="order-con w360 flex  ">
						<view class="fon28 w100">
							身材管理魔体仪
						</view>
						<view class="w100">
							<text class="fon32 color-org">￥{{item.oddt_price}}</text>
							<text class="line-through color9">￥{{item.oddt_dlprice}}</text>
						</view>
						<view class=" color9 line2 w100">
							{{item.desc}}
						</view>
					</view>
					<view class="order-cart">
						<image src="../../static/images/car-icon.png" mode="widthFix" class="w100"></image>
					</view>
				</view>
			</view>
			<!--加载loadding-->
			<tui-loadmore :visible="loadding" :index="3" type="primary"></tui-loadmore>
			<tui-nomore :visible="!pullUpOn"></tui-nomore>
			<!--加载loadding-->
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
				indicatorDots: true,
				autoplay: false,
				interval: 2000,
				duration: 500,
				color: '#fff',
				loop: true,
				proList: [{
						"id": 123,
						"oddt_proname": "身材管理魔体仪",
						"desc": "身材管理魔体仪身材管理魔体仪身材管理魔体仪……",
						"oddt_dlprice": 120,
						"oddt_price": 100,
						"oddt_pic_link": "../../static/images/icon-fenlei.jpg"
					},
					{
						"id": 123,
						"oddt_proname": "身材管理魔体仪",
						"desc": "身材管理魔体仪身材管理魔体仪身材管理魔体仪……",
						"oddt_dlprice": 120,
						"oddt_price": 100,
						"oddt_pic_link": "../../static/images/icon-fenlei.jpg"
					}, {
						"id": 123,
						"oddt_proname": "身材管理魔体仪",
						"desc": "身材管理魔体仪身材管理魔体仪身材管理魔体仪……",
						"oddt_dlprice": 120,
						"oddt_price": 100,
						"oddt_pic_link": "../../static/images/icon-fenlei.jpg"
					}, {
						"id": 123,
						"oddt_proname": "身材管理魔体仪",
						"desc": "身材管理魔体仪身材管理魔体仪身材管理魔体仪……",
						"oddt_dlprice": 120,
						"oddt_price": 100,
						"oddt_pic_link": "../../static/images/icon-fenlei.jpg"
					}
				],
				loadData: [{
						"id": 123,
						"oddt_proname": "身材管理魔体仪",
						"desc": "身材管理魔体仪身材管理魔体仪身材管理魔体仪……",
						"oddt_dlprice": 120,
						"oddt_price": 100,
						"oddt_pic_link": "../../static/images/icon-fenlei.jpg"
					},
					{
						"id": 123,
						"oddt_proname": "身材管理魔体仪",
						"desc": "身材管理魔体仪身材管理魔体仪身材管理魔体仪……",
						"oddt_dlprice": 120,
						"oddt_price": 100,
						"oddt_pic_link": "../../static/images/icon-fenlei.jpg"
					}, {
						"id": 123,
						"oddt_proname": "身材管理魔体仪",
						"desc": "身材管理魔体仪身材管理魔体仪身材管理魔体仪……",
						"oddt_dlprice": 120,
						"oddt_price": 100,
						"oddt_pic_link": "../../static/images/icon-fenlei.jpg"
					}, {
						"id": 123,
						"oddt_proname": "身材管理魔体仪",
						"desc": "身材管理魔体仪身材管理魔体仪身材管理魔体仪……",
						"oddt_dlprice": 120,
						"oddt_price": 100,
						"oddt_pic_link": "../../static/images/icon-fenlei.jpg"
					}
				]
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
				_this.tui.request('/mine/proList', param).then(function(data) {
					_this.loadding = false;
					if (data.stat == 1) {

						_this.pageIndex = data.data.curpage
						_this.pullUpOn = data.data.more;
						_this.proList = _this.proList ? _this.proList.concat(data.data.list) : data.data.list;


					}
				});
			},
		},
		/**
		 * 页面上拉触底事件的处理函数
		 */
		onReachBottom: function() {
			if (!this.pullUpOn) return;
			this.loadding = true;
			if (this.pageIndex == 3) {
				this.loadding = false;
				this.pullUpOn = false;
				
			} else {
				this.proList = this.proList.concat(this.loadData);
				this.pageIndex = this.pageIndex + 1;
				this.loadding = false
			}
		}


	}
</script>

<style lang="scss" scoped>
	.fonb {
		font-family: PingFang-SC-Bold;
	}

	.hello {
		position: relative;
		padding-bottom: 5rpx;
	}

	.hello::after {
		position: absolute;
		width: 92rpx;
		height: 8rpx;
		background-color: #da9e5a;
		content: '';
		left: 0;
		bottom: 0;
	}

	.banner {
		padding: 60rpx 0;
	}

	.video {
		width: 100%;
		height: 100%;
		left: 0;
		top: 0;
		position: absolute;
		border-radius: 20rpx 20rpx 0 0;
	}

	.index-desc {
		line-height: 1.8;
		padding-top: 10rpx;
	}

	.w330 {
		width: 310rpx;
		height: 300rpx;
		margin-bottom: 30rpx;
	}

	.w610 {
		width: 570rpx;
		position: relative;
	}

	.index-about {
		width: 252rpx;
		padding: 15rpx;
		right: -15%;
		top: 50%;
		transform: translateY(-50%);
		background: #fff;
		text-decoration: underline;
		line-height: 1.8;
	}

	.index-list {
		padding-top: 60rpx;
	}

	.w360 {
		width: 360rpx;
		margin: 0 20rpx;
	}

	.list-item {
		padding-top: 20rpx;
	}

	.list-items {
		padding: 30rpx 0;
		border-bottom: 1px solid #f7f5f6;
	}

	.order-cart {
		width: 36rpx;
		display: flex;
		align-items: flex-end;
	}
</style>
