<template>
	<view class="page w100">
		<view class=" w100 padding-lf30">
			<view  class="list-item w100" v-for="(item,index) in infoList" :key="index">
				<view class="flex  flex-just-between flex-al-center">
					<view class="time">
						<view class=" fon28">
							{{item.name}}
						</view>
						<view class=" color9">
							{{item.cmd_addtime}}
						</view>
					</view>
					<view class="content">
						<view class="fon32 color-org">
							{{item.money}}
						</view>
					</view>
				</view>
			</view>
		
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
				infoList: [
					{
					"cmd_addtime": "2019-05-15 12:20",
					"name": "团队订单",
					"money": "+5000"
				},{
					"cmd_addtime": "2019-05-15 12:20",
					"name": "团队订单",
					"money": "+5000"
				},{
					"cmd_addtime": "2019-05-15 12:20",
					"name": "团队订单",
					"money": "+5000"
				},{
					"cmd_addtime": "2019-05-15 12:20",
					"name": "团队订单",
					"money": "+5000"
				}
				],
				loadData: [	{
					"cmd_addtime": "2019-05-15 12:20",
					"name": "333团队订单",
					"money": "+5000"
				},{
					"cmd_addtime": "2019-05-15 12:20",
					"name": "1团队订单",
					"money": "+5000"
				},{
					"cmd_addtime": "2019-05-15 12:20",
					"name": "2团队订单",
					"money": "+5000"
				},{
					"cmd_addtime": "2019-05-15 12:20",
					"name": "团队订单",
					"money": "+5000"
				}],
				loadding: false,
				pullUpOn: true
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
	page{ width: 100%; display: flex;}
	.list-item{ border-bottom: 1px solid #e4e4e4; padding: 40rpx 0;}
</style>
