<template>
	<view class="new">
		<!-- 订单列表 -->
		<view class="new-list">
			<!--新闻列表-->
			<view class="order-item" v-for="(item,index) in orderList" :key="index">
				<view class="top flex flex-al-center flex-just-between">
					<image src="../../static/images/index/icon-touxiang.png" mode="widthFix" class="order-user"></image>
					<view class="order-title">
						<view class=" fon28 flex">
							{{item.name}}

						</view>
						<view class=" color9 fon24">
							ID：{{item.id}}
						</view>
					</view>
					<view class=" user-num  ">
						<view class="flex">
							<view class="">
								销售总额：
							</view>
							<view class=" colorr">
								{{item.total}}
							</view>
						</view>
						<view class="flex">
							直接个数：
							<view class=" color6">
								{{item.num}}
							</view>

						</view>
					</view>
				</view>
			</view>
			<!--新闻列表-->
		</view>

		<!--加载loadding-->
		<tui-loadmore :visible="loadding" :index="3" type="primary"></tui-loadmore>
		<tui-nomore :visible="!pullUpOn"></tui-nomore>
		<!--加载loadding-->
		<!-- end订单列表 -->

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
		props: {
			loadNode: {
				type: Function,
				default: ""
			},
		},
		data() {
			return {
				pageIndex: 1,
				orderList: [{
					img: 1,
					name: "薛定谔的猫",
					id: '88478',
					total: 1560,
					num: 50,
				}, {
					img: 1,
					staus: '已结算',
					name: "1薛定谔的猫",
					id: '88478',
					total: 1560,
					num: 50,

				}, {
					img: 1,
					staus: '已结算',
					name: "薛定谔的猫",
					id: '88478',

					total: 1560,
					num: 50,


				}, {
					img: 1,
					staus: '已结算',
					name: "薛定谔的猫",
					id: '88478',

					total: 1560,
					num: 50,


				}, {
					img: 1,
					staus: '已结算',
					name: "薛定谔的猫",
					id: '88478',

					total: 1560,
					num: 50,


				}, {
					img: 1,
					staus: '已结算',
					name: "薛定谔的猫",
					id: '88478',

					total: 1560,
					num: 50,


				}, {
					img: 1,
					staus: '已结算',
					name: "薛定谔的猫",
					id: '88478',
					total: 1560,
					num: 50,

				}, {
					img: 1,
					name: "薛定谔的猫",
					id: '88478',
					total: 1560,
					num: 50,
				}, {
					img: 1,
					staus: '已结算',
					name: "1薛定谔的猫",
					id: '88478',
					total: 1560,
					num: 50,

				}, {
					img: 1,
					staus: '已结算',
					name: "薛定谔的猫",
					id: '88478',

					total: 1560,
					num: 50,


				}, {
					img: 1,
					staus: '已结算',
					name: "薛定谔的猫",
					id: '88478',

					total: 1560,
					num: 50,


				}, {
					img: 1,
					staus: '已结算',
					name: "薛定谔的猫",
					id: '88478',

					total: 1560,
					num: 50,


				}, {
					img: 1,
					staus: '已结算',
					name: "薛定谔的猫",
					id: '88478',

					total: 1560,
					num: 50,


				}, {
					img: 1,
					staus: '已结算',
					name: "薛定谔的猫",
					id: '88478',

					total: 1560,
					num: 50,


				}, {
					img: 1,
					name: "薛定谔的猫",
					id: '88478',
					total: 1560,
					num: 50,
				}, {
					img: 1,
					staus: '已结算',
					name: "1薛定谔的猫",
					id: '88478',
					total: 1560,
					num: 50,

				}, {
					img: 1,
					staus: '已结算',
					name: "薛定谔的猫",
					id: '88478',

					total: 1560,
					num: 50,


				}],
				loadData: [{
					img: 1,
					staus: '已结算',
					name: "薛定谔的猫",
					id: '88478',

					total: 1560,
					num: 50,


				}, {
					img: 1,
					staus: '已结算',
					name: "薛定谔的猫",
					id: '88478',

					total: 1560,
					num: 50,


				}, {
					img: 1,
					staus: '已结算',
					name: "薛定谔的猫",
					id: '88478',

					total: 1560,
					num: 50,


				}, {
					img: 1,
					staus: '已结算',
					name: "薛定谔的猫",
					id: '88478',

					total: 1560,
					num: 50,


				}, {
					img: 1,
					staus: '已结算',
					name: "薛定谔的猫",
					id: '88478',

					total: 1560,
					num: 50,


				}, {
					img: 1,
					staus: '已结算',
					name: "薛定谔的猫",
					id: '88478',

					total: 1560,
					num: 50,


				}, {
					img: 1,
					staus: '已结算',
					name: "薛定谔的猫",
					id: '88478',

					total: 1560,
					num: 50,


				}],
				loadding: false,
				pullUpOn: true
			}
		},
		onLoad: function(options) {


		},
		mounted() {

		},
		methods: {
			
		},
		/**
		 * 页面相关事件处理函数--监听用户下拉动作
		 */
		onPullDownRefresh: function() {
			//延时为了看效果
			setTimeout(() => {
				this.orderList = this.loadData;
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
			console.log('aa1')
			if (!this.pullUpOn) return;
			this.loadding = true;
			if (this.pageIndex == 3) {
				this.loadding = false;
				this.pullUpOn = false
			} else {
				this.orderList = this.orderList.concat(this.loadData);
				this.pageIndex = this.pageIndex + 1;
				this.loadding = false
			}
		}

	}
</script>

<style lang="scss">
	.new-list {
		padding: 0 30rpx;

		.order-item {
			border-bottom: 1px solid #ececec;
			margin-bottom: 0;
			padding: 30rpx 0;
		}

		.order-user {
			width: 70rpx;
		}

		.user-num {
			width: 180rpx;
		}

		.order-title {
			width: calc(100% - 290rpx);
		}

		.order-desc {
			padding: 25rpx 10rpx;
		}

		.order-img {
			width: 176rpx;
		}

		.order-describe {
			width: 470rpx;
		}

	}
</style>
