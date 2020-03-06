<template>
	<view class="padding-lf30">
		<form @submit="formSubmit" @reset="">
			<view class="label color9">
				绑定微信
			</view>
			<view class="bgf9">
				<input type="text" value="" v-model="dl_weixin" placeholder="请输入微信号" class="fon28  bin-txt" />
			</view>
			
			<button form-type="submit" class="  btns btns-tijiao colorf">确定</button>

		</form>
	</view>
</template>

<script>
	const util = require('../../utils/util.js')
	export default {
		data() {
			return {
dl_weixin:""
			}
		},
		mounted() {	
						this.getData()
		  },
		methods: {
getData(){
				var _this = this
					 _this.tui.request( '/mine/sethead').then(function(data){
					 		if(data.stat == 1){
					 
					 		  _this.dl_weixin = data.data.dl_weixin||""
					 		 
					 		 
					 		}
					 })
			},
			formSubmit: function(e) {
				console.log(e)
				var _this=this
				let dl_weixin = _this.dl_weixin;
				if (util.isNullOrEmpty(dl_weixin)) {
					this.tui.toast('请输入微信号');
					return
				}
				
					let state = {
						dl_weixin: dl_weixin,
							}	
					_this.tui.request( '/mine/edit_weixin',state).then(function(data){
							if(data.stat==1){
								
							}
					})
			},
		}
	}
</script>

<style lang="scss" scoped>
	page{ width: 100%;}
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

</style>
