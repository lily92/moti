<template>
	<view>
		<view class="code-bg positionr">
			<image src="../../static/images/recommand-code.png" mode="widthFix" class="w100"></image>
			<view class="positionb qr-code">
				<image src="../../static/images/qr-code.png" mode="widthFix" class="w100"></image>
			</view>
			<view class="positionb user-img">
				<image src="../../static/images/icon-fenlei.jpg" mode="widthFix" class="w100"></image>
			</view>
			<view class="positionb id">
				ID :158461
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				
			};
		}
	}
</script>

<style lang="scss" scoped>
page{ background: #ffe6bb;}
.qr-code{ width: 400rpx; height:400rpx; z-index: 2; left:183rpx; top:412rpx}
.user-img{ width: 120rpx; height:120rpx; background: #F9F9F9; border-radius: 10rpx; left:340rpx; top:280rpx}
.id{ top:835rpx; width: 100%; text-align: center; left:0}
</style>
