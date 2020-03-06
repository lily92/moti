<template>
	<view class="user-top positionr flex flex-al-center">
		<image src="../../static/images/user/user-top-img.png" mode="widthFix" class="user-top-img positionb"></image>
		<view class="user-desc fon32  colorf ">
			<view class="">
				Hi,
			</view>
			<view class="">
				欢迎来到店主后台
			</view>
		</view>
	</view>
</template>

<script>
</script>


<style lang="scss">
	.user-top {
		width: 750rpx;
		height: 315rpx;
		background: url(~@/static/images/user/user-bg.png) no-repeat center -4rpx;
		background-size: 100%;
		padding-left: 20rpx;
		// background: #000;
		margin-top: -3rpx;

		.user-top-img {
			width: 172rpx;
			right: 38rpx;
			bottom:42rpx;
		}

		.user-desc {
			margin-bottom: 60rpx;
		}

	}
</style>
