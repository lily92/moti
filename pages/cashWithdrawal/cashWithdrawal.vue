<template>
	<view class="padding-lf30 padding-t30">
		<view class="">
			<view class="keti fon26">
				<view class="">
					可提金额
				</view>
				<view class="fon60 keti-fon">
					￥{{data.dl_fanli_recash}}1000
				</view>
			</view>
		<!-- 	<view class=" container flex-al-center shiji">
				<view class=" flex flex-al-center">
					<text class="fon48 color9">￥</text>
					<text class="fon26 colorr">{{data.dl_fanli_recash}}</text>
				</view>
				<view class="fon26 color9 padding-l60">
					<text>实际到账：{{data.dl_fanli_rcreal}}</text>
				</view>
				<view class="fon26 color9 padding-l60">
					<text>手续费：{{data.dl_fanli_rcfee}}</text>
				</view>
			</view>
			<view class="w100 color9 padding-lr20">
				*当前余额{{data.dl_fanli_recash}} 默认全部提现 / 手续费：{{data.ms_withdraw_fee*100}}%
			</view> -->
			<view v-if="data.tixian_text" class="w100 color9 padding-lr20">
				{{data.tixian_text}}
			</view>
		</view>

		<!-- 银行卡信息 -->

		<view class="margin-l30">
			提现
		</view>
		<view class="bank">
			<view class="container lines flex  flex-al-center flex-just-between">
				<view class=" fon42 color9">
					当天余额￥45,596
				</view>
				<view class=" color-org">
					全部提现
				</view>
			</view>
		</view>


		<view class="box-item margin-t30">
			<view class="margin-l30">
				收款人信息
			</view>
			<view @click="goSelect()" v-if="rec_id>0" class="bank">
				<view class="container lines">
					<view class="">
						<input type="text" class="fon24" :value="dreceiptcodelist.rec_name" placeholder="请输入收款人姓名" />
					</view>
				</view>
				<view class="container lines">
					<view class="">
						<input type="text" class="fon24" :value="dreceiptcodelist.rec_account" placeholder="请输入收款账号" />
					</view>
				</view>
				<!-- <view class="container lines">
					<text>收款银行：</text>
					<view class=" positionr">
						<text>{{dreceiptcodelist.rec_bankname}}</text>
						
					</view>
				</view> -->
				<view class="container lines">

					<view class=" positionr">
						<input type="text" class="fon24" :value="dreceiptcodelist.rec_bankname" placeholder="收款银行" />
						<!-- <view class="jiantou">
						</view> -->
					</view>
				</view>
				<!-- 	<view class="container lines">
					<text>银行支行：</text>
					<view class="margin-l30">
						<text>{{dreceiptcodelist.rec_openbranch}}</text>
					</view>
				</view> -->
				<!-- 	<view class="container lines">
					<text>手机号码：</text>
					<view class="margin-l30">
						<text>{{dreceiptcodelist.rec_tel}}</text>
					</view>
				</view> -->

			</view>
		</view>


		<!-- end 银行卡信息 -->


		<navigator v-if="!dreceiptcodelist" class="add-blank flex flex-al-center  text-center" url="./selectBankUse?pick=1">
			<view class="w100">
				<view class="fon40 color9">
					+
				</view>
				<text>选择银行卡</text>
			</view>
		</navigator>
		<view class="text-center tixian-btns">
			<navigator url="../PresentationDetails/PresentationDetails" class="fon32 color-org">提现明细</navigator>
			<button @click="btnPay" type="" class="btns btns-tijiao colorf fon32" form-type="submit">提现</button>
			
		</view>


	</view>
</template>

<script>
	export default {
		data() {
			return {

				dreceiptcodelist: {

				},

				typelist: [], //级别列表

				dlneedinfo: {
					dlni_pinzheng: 0
				},
				wxts: '', //温馨提示
				// 凭证
				file_name: '',
				file_src: '',

				rec_id: 1,
				recitem: {},
				data: {
					dl_tel: '',
					checkcode: '',
				},
				ttamp: '',
				sture: '',
				sdlid: 0,
				loadding: false
			};
		},
		onShow: function() {
			this.getData();
		},
		mounted() {
			this.$eventHub.$on('emit', (data) => {
				setTimeout(() => {
					// this.tui.toast("您选择了：" + data)
					// this.isselect = data
					this.dreceiptcodelist.rec_bankname = data
				}, 350)
			});
			var _this = this
			_this.tui.request('/tools/getsture').then(function(data) {

				if (data.stat == 1) {
					_this.ttamp = data.data.ttamp
					_this.sture = data.data.sture
				}
			});
		},
		methods: {
			toggleTab(str) {
				this.$refs[str].show();
			},
			getData: function() {
				var _this = this
				_this.loadding = true;
				var param = {
					sdlid: _this.sdlid,
					rec_id: uni.getStorageSync("rec_id"),
				}
				_this.tui.request('/fanli/recash', param).then(function(data) {
					_this.loadding = false;
					if (data.stat == 1) {
						_this.data = data.data;
						_this.dreceiptcodelist = data.data.dreceiptcodelist
						_this.rec_id = _this.dreceiptcodelist.rec_id || 0

					} else if (data.stat == 2) {
						_this.tui.toast('请前往设置银行卡信息')
						setTimeout(() => {
							// this.tui.toast("您选择了：" + data)
							uni.navigateTo({
								url: "/pages/cashWithdrawal/selectBankUse?pick=1"
							})
						}, 350)
					}
				});
			},
			goSelect() {
				uni.navigateTo({
					url: "/pages/cashWithdrawal/selectBankUse?pick=1"
				})
			},
			btnPay() {
				var _this = this
				if (_this.rec_id <= 0) {
					this.tui.toast('请选择银行卡信息');
					return false;
				}
				if (_this.data.tixian_mini > _this.data.dl_fanli_recash) {
					this.tui.toast('最小提现金额为' + _this.data.tixian_mini + '元');
					return false;
				}
				uni.showModal({
					title: "申请提现",
					content: "确认申请提现?",
					success: function(res) {
						if (res.confirm) {

							_this.loadding = true;
							var param = {
								ttamp: _this.ttamp,
								sture: _this.sture,
								rec_id: _this.rec_id,
								dl_tel: _this.data.dl_tel,
								sdlid: _this.data.sdlid,
								checkcode: _this.data.checkcode,
							}
							_this.tui.request('/fanli/recashsave', param).then(function(data) {
								_this.loadding = false;
								if (data.stat == 1) {
									// uni.navigateTo({
									// 	url: "/pages/extend-view/mall-extend/my/applylist?currentTab=1"
									// })
									uni.navigateTo({
										url: "/pages/cashWithdrawal/presentationDetails"
									})

								}
							});
						} else if (res.cancel) {
							console.log('用户点击取消');
						}
					}
				});

			},

		}
	}
</script>

<style lang="scss" scoped>
	page {
		width: 100%;
	}

	.tixian-top {
		width: 100%;
		height: 268rpx;
		background-color: #ffffff;
		box-shadow: 0rpx 0rpx 16rpx 0rpx rgba(144, 160, 228, 0.11);
		border-radius: 10rpx;
	}

	.keti {
		padding: 60rpx;
		background: #000;
		border-radius: 20rpx;
		color: #fff;
		margin-bottom: 30rpx;
		background: url(~@/static/images/tixain-bg.png) no-repeat center; background-size: 100%;
	}

	.shiji {
		padding: 0 20rpx;
		border-bottom: 1rpx solid #E6E6E6;
		padding-bottom: 20rpx;
		margin-bottom: 20rpx;
	}

	.tx-btn {
		width: 498rpx;
		height: 80rpx;
		background-image: linear-gradient(67deg,
			#da9e5a 0%,
			#f4d195 100%),
			linear-gradient(#dda461,
			#dda461);
		background-blend-mode: normal,
			normal;
		border-radius: 20rpx;
		margin-bottom: 30rpx;
	}

	.tixian-btns {
		width: 100%;
		margin: 30rpx auto;
	}

	.add-blank {
		width: 100%;
		height: 180rpx;
		background-color: #ffffff;
		box-shadow: 0rpx 0rpx 16rpx 0rpx rgba(144, 160, 228, 0.11);
		border-radius: 10rpx;
		margin-top: 60rpx;
	}

	.bank {
		margin-top: 30rpx;
		background-color: #ffffff;
		box-shadow: 0rpx 0rpx 16rpx 0rpx rgba(144, 160, 228, 0.11);
		border-radius: 10rpx;
		padding: 20rpx 20rpx 40rpx;
		display: block;
	}

	.lines {
		border-bottom: 1rpx solid #E6E6E6;
		padding: 20rpx 0;
	}

	.margin-l30 {
		margin-left: 30rpx;
		width: calc(100% - 160rpx);
	}

	.tx-txt {
		width: 100%;
	}

	.jiantou {
		width: 24rpx;
		height: 44rpx;
		// background: url(../../static/images/cashWithdrawal/jiantou.png) no-repeat center;
		background-size: 12rpx 22rpx;
		position: absolute;
		right: 0;
		top: 50%;
		transform: translateY(-50%);
	}

	.keti-fon {
		padding: 50rpx 0 0 0;
	}

	page {
		background: #f9f9f9;
	}
	.margin-t30{ margin-top: 30rpx;}
	uni-input{ height:1.8em; line-height: 1.8em;}
	
</style>
