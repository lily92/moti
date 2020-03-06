<template>
	<view class="padding-lf30">
		<form @submit="formSubmit">
			<view class="label color9">
				绑定新手机
			</view>
			<view class="bgf9">
				<input type="number" v-model="mobile" value="" placeholder="请输入新手机号码" class="fon28  bin-txt" />
			</view>
			<view class="label color9">
				验证码
			</view>
			<view class="bgf9 ">
				<view class="flex flex-al-between flex-al-center line">
					<input type="number" v-model="code" value="" placeholder="请输入验证码" class="fon28  code-width " />
					<view class="send-code colorp" @click="btnSend">
						{{btnText}}
					</view>
				</view>
			</view>
			<view class="label color9">
				登录密码
			</view>
			<view class="bgf9">
				<input type="password" v-model="password" value="" placeholder="请输入登录密码" class="fon28  bin-txt" />
			</view>
			<button form-type="submit" class="btns btns-tijiao colorf">确定</button>

		</form>
	</view>
</template>

<script>
	const util = require('../../utils/util.js')
	export default {
		data() {
			return {
			btnText: "发送验证码",
			disabled:false,
			mobile: "",//账号
			ttamp: '',//时间戳
			sture: '',//隐藏提交,验证是否超时,
			code: "",//验证码
			password: "",//密码
			}
		},
		mounted() {
					
					   var _this = this
					         _this.tui.request( '/tools/getsture').then(function(data){
					    
					           if(data.stat == 1){
					             _this.ttamp = data.data.ttamp
					             _this.sture = data.data.sture
					           }
					         });
		  },
		methods: {
btnSend: function() {
				if(this.disabled){
					return
				}
				if (util.isNullOrEmpty(this.mobile)) {
					this.tui.toast('请输入手机号码');
					return
				} else if (!util.isMobile(this.mobile)) {
					this.tui.toast('请输入正确的手机号码');
					return
				}
				this.disabled = true;
				this.btnText = "请稍候...";
				this.type = "gray"
				let seconds=60
						let countdown = setInterval(() => {
							if (seconds > 0) {
								this.btnText = seconds + "s后获取"
									--seconds;
							} else {
								this.btnText = "获取验证码";
								this.disabled = false;
								this.type = "primary";
								clearInterval(countdown);
							}
						}, 1000);	
							let param = {
								dl_tel: this.mobile,
								type:3,
							};
				this.tui.request( '/login/getVertifyCode',param).then(function(data){
						if(data.stat==1){
						}
				})
				// let code = this.getRandom(6);
				// this.tui.toast('您本次的验证码是：' + code, 5000);
			},
			formSubmit: function(e) {
				console.log(e)
				var _this=this
				let code = _this.code;
				let mobile = _this.mobile;
				let pwd = _this.password;
				if (util.isNullOrEmpty(mobile)) {
					this.tui.toast('请输入手机号码');
					return
				}else if (!util.isMobile(mobile)) {
					this.tui.toast('请输入正确的手机号码');
					return
				} else if (util.isNullOrEmpty(code)) {
					this.tui.toast('请输入验证码');
					return
				} else if (util.isNullOrEmpty(pwd)) {
					this.tui.toast('请输入登录密码');
					return
				} 
				
					let state = {
						tel: mobile,
						pwd:_this.MD5.hexMD5(pwd),
						ttamp:_this.ttamp,
						sture:_this.sture,
						code:_this.code,
						type:0,
							}	
					_this.tui.request( '/mine/edit_tel',state).then(function(data){
							if(data.stat==1){
								_this.tui.toast("修改成功，请重新登录")
								setTimeout(function (){
									uni.clearStorage()
									_this.$store.commit('logout')
									uni.reLaunch({
										url: getApp().globalData.loginType
									})
									 }, 500)
							}
					})
			},
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
</style>
