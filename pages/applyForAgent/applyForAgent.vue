<template>
	<view>
		<form @submit="" @reset="">
			<view class="flex flex-just-between padding-lf30 top">
				<view class="tab-item">
					运营商
				</view>
				<view class="tab-item">
					代理商
				</view>
				<view class="tab-item active">
					合伙人
				</view>
			</view>
			<view class="bgf9 padding-lf30">
				<view class="item">
					<view class="fon24">
						个人信息
					</view>
					<view class="box bgf">
						<view class="">
							<input type="text" value="" placeholder="请输入姓名" class="fon28 txt" />
						</view>
						<view class="">
							<input type="text" value="" placeholder="请输入手机号码" class="fon28 txt" />
						</view>
						<view class="">
							<input type="text" value="" placeholder="请输入邮箱地址" class="fon28 txt" />
						</view>
					</view>
				</view>
				<view class="item">
					<view class="fon24">
						银行卡
					</view>
					<view class="box bgf">
						<view class="">
							<input type="text" value="" placeholder="请输入银行卡号" class="fon28 txt" />
						</view>
					</view>
				</view>
				<view class="item">
					<view class="fon24">
						合同编号
					</view>
					<view class="box bgf">
						<view class="">
							<input type="text" value="" placeholder="请输入合同编号" class="fon28 txt" />
						</view>
					</view>
				</view>
				<view class="item">
					<view class="fon24">
						身份证
					</view>
					<view class=" color9 flex flex-just-between">
						<view class="identity-img flex flex-al-center  text-center ">
							<view class='w100'>
								<view class="add">
									+
								</view>
								<view class="">
									上传正面
								</view>
							</view>
						</view>
						<view class="identity-img flex flex-al-center  text-center ">
							<view class='w100'>
								<view class="add">
									+
								</view>

								<view class="">
									上传正面
								</view>
							</view>
						</view>
					</view>
				</view>
				<view class="item">
					<view class="fon24">
						营业执照
					</view>
					<view class=" color9 flex flex-just-between">
						<view class="identity-img flex flex-al-center  text-center  w100 ">
							<view class='w100'>
								<view class="add">
									+
								</view>
								<view class="">
									上传营业执照
								</view>
							</view>
						</view>
				
					</view>
				</view>

			</view>
			<button form-type="submit" class="btn btn-tijiao">确认</button>

		</form>
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
	.top {
		margin-bottom: 30rpx;
	}

	.tab-item {
		width: 138rpx;
		height: 60rpx;
		line-height: 60rpx;
		border-radius: 30rpx;
		text-align: center;
	}

	.tab-item.active,
	.tab-item:hover {
		background-image: linear-gradient(67deg,
			#da9e5a 0%,
			#f4d195 100%),
			linear-gradient(#000000,
			#000000);
		background-blend-mode: normal,
			normal;
		color: #fff;
	}

	.item {
		padding: 65rpx 0 0 0;
	}

	.bgf {
		background: #fff;
	}

	.box {
		border-radius: 20rpx;
		padding: 0 30rpx 40rpx;
		margin-top: 20rpx;
	}

	.txt {
		padding: 20rpx 10rpx;
		border-bottom: 1px solid #e4e4e4;
		height: 100rpx;
		width: 100%;
		font-size: 28rpx;
	}

	.identity-img {
		width: 48%;
		height: 228rpx;
		background-color: #ffffff;
		border-radius: 20rpx;
		margin-top: 30rpx;
	}

	.add {font-size: 80rpx;}
	.identity-img.w100{ width: 100%;}
	

</style>
