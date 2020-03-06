<template>
	<view class="padding-lf30">
		<view class="person-top flex flex-al-center  flex-just-between">
			<view class="">
				<view class=" color0  fon80 ">
					游客
				</view>
				<view class="color9 fon32">
					ID:223531
				</view>
			</view>
			<view class="person-touxiang">
				<image src="../../static/images/user/icon-touxing.png" mode="widthFix" class="w100"></image>
			</view>
		</view>

		<view class="">
			<form @submit="" @reset="" class="form">
				<view class="">
					<input type="password" value="" placeholder="请输入新微信" class="txt pwd-icon" />
					<button type="" class="btn colorf" >确认修改</button>
				</view>
			</form>

		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {

			};
		},
		methods: {
		
		},
		mounted() {
			
		}

	}
</script>
<style lang="scss" scoped>
	.txt {
		width: 648rpx;
		height: 80rpx;
		line-height: 80rpx;
		background-color: #ffffff;
		box-shadow: 0rpx 1rpx 5rpx 0rpx rgba(0, 0, 0, 0.17);
		border-radius: 40rpx;
		border: solid 1rpx #ebebeb;
		padding-left: 55rpx;
		margin: 0 auto 40rpx;
	}

	.pwd-icon {
		background: url(~@/static/images/user/icon-pwd.png) no-repeat 20rpx center;
		background-size: 20rpx 32rpx
	}

	.person-top {
		padding-top: 60rpx;
		padding-bottom: 200rpx;
	}

	.person-touxiang {
		width: 128rpx;
		height: 128rpx;
		border-radius: 50%;
		background: #90a0e4;
		margin-right: 35rpx;
	}

	.btn {
		width: 606rpx;
		height: 86rpx;
		background-image: linear-gradient(90deg,
			#766eff 0%,
			#bd95ff 100%),
			linear-gradient(#1f6ecf,
			#1f6ecf);
		background-blend-mode: normal,
			normal;
		box-shadow: 0rpx 12rpx 16rpx 0rpx rgba(28, 100, 224, 0.32);
		border-radius: 43rpx;
	}
</style>
