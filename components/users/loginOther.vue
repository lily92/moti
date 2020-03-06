<template>
	<view class="" >
		<view class="login-other text-center fon22 positionr">
			使用第三方账号登录
		</view>
		<view class="icon-wechat" @click="wxlogin(1)" >
			<image src="../../static/images/user/icon-wechat.png" mode="widthFix" class="w100"></image>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
			};
		},
		mounted() {
		},
		methods: {
			  	wxlogin(index){
					console.log(index)
					this.$emit('wxlogin',index);
					}
		}
		}

</script>

<style lang="scss">
	.login-other{ color:#808080 ;  width: 220rpx; margin: 40rpx auto 0;}
	.login-other::before,.login-other::after{ display: block; content:''; width: 60rpx; position: absolute; top:50%; transform: translateY(-50%); height:1rpx; background: #808080;}
	.login-other::before{left: -70rpx;}
	.login-other::after{right: -70rpx;}
	.icon-wechat{ width: 66rpx; margin: 25rpx auto;}
</style>
