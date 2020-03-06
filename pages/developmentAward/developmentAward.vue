<template>
	<view class="page w100">
		<view class=" w100 padding-lf30">
			<view class="list-item w100" v-for="(item,index) in infoList" :key="index">
				<view class="flex  flex-just-between flex-al-center">
					<view class="time">
						<view class=" fon28">
							{{item.name}} <text class="color9">({{item.nickName}})</text>
						</view>
						<view class=" color9 time">
							{{item.cmd_addtime}}
						</view>
						<view class="color9">
							TEL:{{item.tel}}
						</view>
					</view>
					<view class="content">
						<view class=" colorr fon24">
							{{item.describe}}
						</view>
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
				infoList: [{
					"cmd_addtime": "2019-05-15 12:20",
					"name": "运营商",
					"money": "+5000",
					"nickName": "李柒凛",
					"tel": '15226530768',
					"describe":""
				}, {
					"cmd_addtime": "2019-05-15 12:20",
					"name": "代理商",
					"money": "+5000",
					"nickName": "李柒凛",
					"tel": '15226530768',
					"describe":""
				}, {
					"cmd_addtime": "2019-05-15 12:20",
					"name": "运营商",
					"money": "+5000",
					"nickName": "李柒凛",
					"tel": '15226530768',
					"describe":"间推首单"
				}],
				loadData: [{
					"cmd_addtime": "2019-05-15 12:20",
					"name": "运营商",
					"money": "+5000",
					"nickName": "李柒凛",
					"tel": '15226530768',
					"describe":"间推首单"
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
	page {
		width: 100%;
		display: flex;
	}

	.list-item {
		border-bottom: 1px solid #e4e4e4;
		padding: 40rpx 0;
	}

	.time {
		padding: 5rpx 0;
	}
</style>
