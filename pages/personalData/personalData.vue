<template>
	<view class="padding-lf30">
		<view class="logout colorf" @click="logout">
			退出登录
		</view>

		<image-cropper :src="tempFilePath" @confirm="confirm" @cancel="cancel"></image-cropper>

		<form @submit="" @reset="">
			<view class="touxaing flex flex-al-center flex-just-between">
				<view class="color9">
					头像
				</view>
				<view class="flex flex-al-center">
					<view class="touxaing-icon">
						<image src="../../static/images/icon-fenlei.jpg" mode="widthFix" class="w100"></image>
					</view>
					<view class="mores">
						<image src="../../static/images/common/icon-more.png" mode="widthFix" class="more-img"></image>
					</view>
				</view>


			</view>
			<view class="label color9">
				联系号码
			</view>
			<view class="bgf9 positionr">
				<view class="bin-txt">
					{{dl_tel_str}}
				</view>
				<view @click="editTel" class="more positionb">

				</view>
			</view>
			<view class="label color9">
				微信号
			</view>
			<view class="bgf9 ">
				<view class="flex flex-al-between flex-al-center line">
					<view class="fon28  code-width ">{{password?"******":'尚未设置微信'}} </view>
					<navigator class="send-code colorp" url="../bindWechat/bindWechat">
						{{password?"修改微信":'去设置微信'}}
					</navigator>
				</view>
			</view>
			<view class="label color9">
				收货地址
			</view>
			<view class="bgf9 positionr">
				<view class="bin-txt">
					{{dl_weixin}}
				</view>
				<view @click="editAddess" class="more positionb">

				</view>
			</view>
			<!-- <button form-type="submit" class="btn-submit colorf">确定</button> -->

		</form>
	</view>
</template>

<script>
	import ImageCropper from "@/components/invinbg-image-cropper/invinbg-image-cropper.vue";

	export default {
		components: {
			ImageCropper
		},
		data() {
			return {
				cropFilePath: "../../static/images/icon-fenlei.png",
				tempFilePath: '',
				dl_tel_str: "13719150488",
				dl_weixin: "",
				password: "",
				ttamp: "", //时间戳
				sture: '', //隐藏提交,验证是否超时,

			}
		},
		mounted() {
			var _this = this
			_this.tui.request('/mine/sethead').then(function(data) {
				if (data.stat == 1) {
					_this.cropFilePath = data.data.dl_headimg_link
					_this.dl_tel_str = data.data.dl_tel_str
					_this.password = data.data.dl_pwd
					_this.dl_weixin = data.data.dl_weixin
				}
			})
		},
		methods: {
			logout: function() { //退出登录
				uni.showModal({
					title: '提示',
					content: '确定退出登录？',
					confirmColor: '#5677FC',
					success: (res) => {
						if (res.confirm) {
							uni.clearStorage()
							this.$store.commit('logout')
							uni.reLaunch({
								url: getApp().globalData.loginType
							})
						}
					}
				});
			},
			upload() {
				var _this = this
				_this.tui.request('/tools/getsture').then(function(data) {

					if (data.stat == 1) {
						_this.ttamp = data.data.ttamp
						_this.sture = data.data.sture
					}
				}); //先获取时间戳
				uni.chooseImage({
					count: 1, //默认9
					sizeType: ['original', 'compressed'], //可以指定是原图还是压缩图，默认二者都有
					sourceType: ['album'], //从相册选择
					success: (res) => {
						this.tempFilePath = res.tempFilePaths.shift()
					}
				});
			},
			confirm(e) {
				var _this = this
				_this.tempFilePath = ''


				_this.tui.uploadFile(e.detail.tempFilePath, _this.ttamp, _this.sture).then(function(data) {

					if (data.stat == 1) {
						_this.cropFilePath = e.detail.tempFilePath

						let state = {
							action: 'save',
							dl_headimg: data.savename,
						};
						_this.tui.request('/mine/sethead', state).then(function(data) {

						})
					}
				})
			},
			cancel() {
				console.log('canceled')
			},
			editTel() {
				uni.navigateTo({
					url: "../setting/bindPhone"
				})
			},
			editAddess() {
				uni.navigateTo({
					url: "../address/addAdress"
				})
			}
		}
	}
</script>

<style lang="scss" scoped>
	.bgf9 {
		background-color: #f9f9f9;
		border-radius: 10rpx;
		padding: 30rpx;
		margin-top: 30rpx;
		margin-bottom: 60rpx;
	}

	.btn-submit {
		width: 335rpx;
		lin-height: 80rpx;
		background-color: #90a0e4;
		box-shadow: 0rpx 0rpx 13rpx 0rpx rgba(144, 160, 228, 0.1);
		border-radius: 10rpx;
		position: absolute;
		bottom: 60rpx;
		left: 50%;
		transform: translateX(-50%);
	}

	.bin-txt {
		padding: 30rpx 0;
		border-bottom: 1px solid #e4e4e4;
		box-sizing: content-box;
	}

	.code-width {
		width: 500rpx;
	}

	.line {
		padding-bottom: 30rpx;
		border-bottom: 1px solid #e4e4e4;
	}

	.more {
		right: 20rpx;
		top: 50%;
		transform: translateY(-50%);
		width: 4rpx;
		height: 19rpx;
		background: url(~@/static/images/common/icon-more.png);
		background-size: 4rpx 19rpx;
	}

	.touxaing-icon {
		width: 100rpx;
		height: 100rpx;
		background: #000;
		border-radius: 10rpx;
	}

	.select-icon {
		width: 49rpx;
		height: 49rpx;
		bottom: -10rpx;
		left: -10rpx;
	}
	.mores{margin-left: 20rpx;}
	.more-img {
		width: 4rpx;
	}
</style>
