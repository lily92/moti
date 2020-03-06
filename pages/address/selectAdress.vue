<template>
	<view class="padding-lf30 padding-t30">
		<view class="uni-list ">
			<radio-group>
				<label  class=" flex flex-al-center flex-just-between bgf items" v-for="(item, index) in addressList" :key="index">
					<view @click="pickAddr(item.dladd_id)">
						<radio :value="item.dladd_id.toString()" :checked="item.dladd_default===1" color="#dda461" />
					</view>
					<view class="item-desc">
						<view @click="pickAddr(item.dladd_id)">
							<text class="fon28">{{item.dladd_contact}} </text> 
							<text  class="tel">{{item.dladd_tel}}</text>
						</view >
						<view @click="pickAddr(item.dladd_id)" class=" color9">
							{{item.dladd_address}}
						</view>
					</view>
					<view  @click="editAddr(item.dladd_id)" class="more">

					</view>
				</label>
			</radio-group>

		</view>
		<view  class="btns btns-tijiao colorf text-center margin-auto" @click="editAddr(0)">添加新地址</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				addressList: [
					{
						"dladd_contact":"唐汉网络",
						"dladd_address":"12121",
						"dladd_tel":"13719150488",
						"dladd_default":1,
						"dladd_id":12121
					},{
						"dladd_contact":"唐汉网络",
						"dladd_address":"12121",
						"dladd_tel":"13719150488",
						"dladd_default":0,
						"dladd_id":12121
					}
				],
				pick:0,
				current: 0,
			};
		},
		onLoad: function(options) {
		this.pick=options.pick||0;
				},
				onShow: function() {
					// this.getData();
				},
		methods: {
			radioChange: function(evt) {
				var _this=this;
				for (let i = 0; i < this.addressList.length; i++) {
					if (this.addressList[i].value === evt.target.value) {
						this.current = i;
						if(_this.pick){
							uni.setStorageSync("dladd_id", evt.target.value);
							uni.navigateBack({
							    delta: 1
							});
						}
						break;
					}
				}
			},
			editAddr(index, addressType) {
					uni.navigateTo({
						url: "../address/addAdress?dladd_id="+index
					})
				},
				pickAddr(index){
					var _this=this;
					if(_this.pick){
						uni.setStorageSync("dladd_id", index);
						uni.navigateBack({
						    delta: 1
						});
					}
				},
				getData:function(){
					var _this = this
					_this.loadding=true;
					var param={
					}
					      _this.tui.request( '/mine/dladdresslist',param).then(function(data){
					       _this.loadding=false;
							if(data.stat == 1){
							  _this.addressList=data.data;
							  
							}
					      });
				},
			},
	
	}
</script>

<style lang="scss" scoped>
	.bgf {
		background: #fff;
	}

	page {
		background: #F7F7F7
	}

	.items {
		margin-bottom: 30rpx;
		padding: 30rpx;
	}

	.item-desc {
		width: calc(100% - 100rpx);
	}

	.more {
		width: 8rpx;
		background: url(~@/static/images/common/icon-more.png) no-repeat center;
		height: 38rpx;
		background-size: 4rpx 19rpx
	}


	.tel{ padding-left: 10rpx;}
</style>
