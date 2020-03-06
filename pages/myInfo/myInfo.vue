<template>
	<view class="page bgf9 ">

		<!-- 订单列表 -->
		<view class="info-list w100 padding-lf30">
			<!--消息列表-->
			<navigator :url="'./detail?cmd_id='+item.cmd_id" class="info-item" v-for="(item,index) in infoList" :key="index">
				<view class="top flex  flex-just-between">
					<view class="time color9">
						<view class=" fon30 color0">
							{{item.cmd_addtime_year}}
						</view>
						<view class="">
							{{item.cmd_addtime_md}}
						</view>
					</view>
					<view class="content">
						<view class="fon32 title">
							{{item.cmd_title}}
						</view>
						<view class="fon26 color6 cmd_des ">
							{{item.cmd_des}}
						</view>
					</view>

				</view>
			</navigator>
			<!--消息列表-->
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
		data() {
			return {
				pageIndex: 0,
				loadding: false,
				pullUpOn: true,
				infoList: [{
					"cmd_addtime_year": "2019",
					"cmd_addtime_md": "02-15",
					"cmd_title": "魔体系统通知",
					"cmd_des": "系统升级，升级时间为219年11月23日14：30-11月24日14：30，升级期间app暂时不可使用，如有紧急问题请及时联系客服进行处理，望请谅解！",
					"cmd_id": "15"
				}, {
					"cmd_addtime_year": "2019",
					"cmd_addtime_md": "02-15",
					"cmd_title": "魔体系统通知",
					"cmd_des": "系统升级，升级时间为219年11月23日14：30-11月24日14：30，升级期间app暂时不可使用，如有紧急问题请及时联系客服进行处理，望请谅解！",
					"cmd_id": "15"
				}, {
					"cmd_addtime_year": "2019",
					"cmd_addtime_md": "02-15",
					"cmd_title": "魔体系统通知",
					"cmd_des": "系统升级，升级时间为219年11月23日14：30-11月24日14：30，升级期间app暂时不可使用，如有紧急问题请及时联系客服进行处理，望请谅解！",
					"cmd_id": "15"
				}],
				loadData: [{
					"cmd_addtime_year": "2019",
					"cmd_addtime_md": "02-15",
					"cmd_title": "11测试刷新",
					"cmd_des": "系统升级，升级时间为219年11月23日14：30-11月24日14：30，升级期间app暂时不可使用，如有紧急问题请及时联系客服进行处理，望请谅解！",
					"cmd_id": "15"
				}, {
					"cmd_addtime_year": "2019",
					"cmd_addtime_md": "02-15",
					"cmd_title": "22测试刷新",
					"cmd_des": "系统升级，升级时间为219年11月23日14：30-11月24日14：30，升级期间app暂时不可使用，如有紧急问题请及时联系客服进行处理，望请谅解！",
					"cmd_id": "15"
				}, {
					"cmd_addtime_year": "2019",
					"cmd_addtime_md": "02-15",
					"cmd_title": "魔体系统通知",
					"cmd_des": "系统升级，升级时间为219年11月23日14：30-11月24日14：30，升级期间app暂时不可使用，如有紧急问题请及时联系客服进行处理，望请谅解！",
					"cmd_id": "15"
				}],
				
			}
		},
		onLoad: function(options) {


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
				_this.tui.request('/mine/infoList', param).then(function(data) {
					_this.loadding = false;
					if (data.stat == 1) {

						_this.pageIndex = data.data.curpage
						_this.pullUpOn = data.data.more;
						_this.infoList = _this.infoList ? _this.infoList.concat(data.data.list) : data.data.list;


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
				this.infoList = this.loadData;
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
			if (this.pageIndex == 3) {
				this.loadding = false;
				this.pullUpOn = false
			} else {
				this.infoList = this.infoList.concat(this.loadData);
				this.pageIndex = this.pageIndex + 1;
				this.loadding = false
			}
		}

	}
</script>

<style lang="scss" scoped>
	page {
		background: #F9F9F9
	}

	.info-item {
		width: 100%;
		min-height: 264rpx;
		background-color: #ffffff;
		box-shadow: 0px 3rpx 8rpx 0px rgba(0, 0, 0, 0.06);
		border-radius: 8rpx;
		padding: 30rpx;
		margin-bottom: 40rpx;
	}

	.time {
		width: 70rpx;
	}

	.content {
		width: calc(100% - 112rpx);
	}

	.cmd_des {
		padding-top: 10rpx;
	}
</style>
