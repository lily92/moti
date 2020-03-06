<template>
	<view class="tui-addr-box">
		<w-picker
			mode="region"
			:areaCode="areaCode"
			:hideArea="false"
			@confirm="onConfirm" 
			ref="region"
			:timeout="true"
		></w-picker>
		<form :report-submit="true">
			<tui-list-cell :hover="false" padding="0">
				<view class="tui-line-cell">
					<view class="tui-title">收货人</view>
					<input placeholder-class="tui-phcolor" class="tui-input" v-model="dladd_contact" name="dladd_contact" placeholder="请输入收货人姓名" maxlength="15" type="text" />
				</view>
			</tui-list-cell>
			<tui-list-cell :hover="false" padding="0">
				<view class="tui-line-cell">
					<view class="tui-title">手机号码</view>
					<input placeholder-class="tui-phcolor" class="tui-input" v-model="dladd_tel" name="dladd_tel" placeholder="请输入收货人手机号码" maxlength="11"
					 type="text" />
				</view>
			</tui-list-cell>
			<tui-list-cell :arrow="true" padding="0">
				<view class="tui-line-cell">
					<view class="tui-title"><text class="tui-title-city-text">所在城市</text></view>
					<input @tap="toggleTab('region')" placeholder-class="tui-phcolor" v-model="dladd_diqustr" class="tui-input" disabled name="city" placeholder="请选择城市" maxlength="50" type="text" />
				</view>
			</tui-list-cell>
			
			<tui-list-cell :hover="false" padding="0">
				<view class="tui-line-cell">
					<view class="tui-title">收货地址</view>
					<input placeholder-class="tui-phcolor" class="tui-input" v-model="dladd_address" name="dladd_address" placeholder="请输入详细的收货地址" maxlength="50" type="text" />
				</view>
			</tui-list-cell>
			<!-- <tui-list-cell :hover="false" padding="0">
				<view class="tui-line-cell">
					<view class="tui-cell-title">地址类型</view>
					<view class="tui-addr-label">
						<text v-for="(item,index) in lists" :key="index" class="tui-label-item" :class="{'tui-label-active':index==1}">{{item}}</text>
					</view>
				</view>
			</tui-list-cell> -->

			<!-- 默认地址 -->
			<tui-list-cell :hover="false" padding="0">
				<view class="tui-swipe-cell">
					<view>设为默认地址</view>
					<switch  :checked="dladd_default?true:false" @change="switchChange" color="#90A0E4" class="tui-switch-small" />
				</view>
			</tui-list-cell>
			<!-- 保存地址 -->
			<view @click="onSave" class="tui-addr-save">
				<tui-button height="88rpx" class="btn-save">保存收货地址</tui-button>
			</view>
			<view @click="onDelete" class="tui-del" v-if="dladd_id>0">
				<tui-button type="gray" height="88rpx">删除收货地址</tui-button>
			</view>
		</form>
	</view>
</template>

<script>
	import wPicker from "@/components/w-picker/w-picker.vue";
	import tuiButton from "@/components/extend/button/button"
	import tuiListView from "@/components/list-view/list-view"
	import tuiListCell from "@/components/list-cell/list-cell"
	export default {
		components: {
			tuiButton,
			tuiListView,
			tuiListCell,
			wPicker,
		},
		data() {
			return {
				lists: ["公司", "家", "学校", "其他"],
				dladd_id: 0,//地址id
				dladd_contact:"",
				dladd_address:"",
				dladd_diqustr:"",
				dladd_default:1,
				dladd_tel:"",
				region:"",
				resultInfo:"",
				dladd_sheng:"",
				dladd_shi:"",
				dladd_qu:"",
				areaCode:[],
				
			}
		},
		onLoad: function(options) {
			console.log(options); //打印出上个页面传递的参数。
			this.dladd_id=options.dladd_id||0;
			
		},
		computed: {
		    // 计算属性
		    distr : function () {
				
					 return 1
						
			}
			},
		mounted() {
			if(this.dladd_id!='0'){
			//if(this.dladd_id=6){
				this.getData();
			}
		  },
		methods: {
			toggleTab(str){
				this.$refs[str].show();
			},
			getData:function(){
				var _this = this
				_this.loadding=true;
				var param={
					'dladd_id': this.dladd_id,
				}
				      _this.tui.request( '/mine/getaddress',param).then(function(data){
				       _this.loadding=false;
						if(data.stat == 1){
						  _this.dladd_contact=data.data.dladd_contact;
						  _this.dladd_tel=data.data.dladd_tel;
						  _this.dladd_address=data.data.dladd_address;
						  _this.dladd_default=data.data.dladd_default;
						  _this.dladd_diqustr=data.data.dladd_diqustr;
						  _this.dladd_sheng = data.data.dladd_sheng.toString();
						  _this.dladd_shi = data.data.dladd_shi.toString();
						  _this.dladd_qu = data.data.dladd_qu.toString();
						  _this.areaCode = [_this.dladd_sheng,_this.dladd_shi,_this.dladd_qu];
						  
						  
						}
				      });
			},
			onSave() {
				//提交表单
				if(this.dladd_contact == ''){
					this.tui.toast("请输入收件人")
					return false;
				}
				if(this.dladd_tel == ''){
					this.tui.toast("请输入手机")
					return false;
				}
				if(this.dladd_diqustr == ''){
					this.tui.toast("请选择所在地区")
					return false;
				}
				if(this.dladd_address == ''){
					this.tui.toast("请输入收货地址")
					return false;
				}
				var _this = this;
				var param = {
					'action': this.dladd_id!='0'?'edit':'add',
					'dladd_id': this.dladd_id,
					'dladd_contact': this.dladd_contact,
					'dladd_tel': this.dladd_tel,
					'dladd_sheng': this.dladd_sheng,
					'dladd_shi': this.dladd_shi,
					'dladd_qu': this.dladd_qu,
					'dladd_diqustr': this.dladd_diqustr,
					'dladd_address': this.dladd_address,
					'dladd_default': this.dladd_default,
				};
				_this.tui.request('/mine/addresssave',param).then(function(data){
					if(data.stat == 1){
						uni.navigateBack({
						    delta: 1
						});
					}else if(data.stat == 0){
						
					}else if(data.stat == 9){
						
					}
				})
			},
			onDelete() {
				var _this = this;
				uni.showModal({
				    title: '删除地址',
				    content: '是否确认删除地址',
				    success: function (res) {
				        if (res.confirm) {
							
				            console.log('用户点击确定');
							
							var param = {
								'dladd_id': _this.dladd_id,
							}
							_this.tui.request('/mine/deladdress',param).then(function(data){
								if(data.stat == 1){
									uni.navigateBack({
									    delta: 1
									});
								}else if(data.stat == 0){
									
								}else if(data.stat == 9){
									
								}
							})
				        } else if (res.cancel) {
				            console.log('用户点击取消');
				        }
				    }
				});
			},
			switchChange (e) {
						let value = e.target.value
						console.log(value)
						let that = this
						this.$set(that, 'dladd_default', value)   // 将点击改变的状态赋给dladd_default
						},
						toArr(object) {
							let arr = [];
							for (let i in object) {
								arr.push(object[i].name);
							}
							return arr;
						},
						onConfirm(val){
							console.log(val);
							//如果页面需要调用多个mode类型，可以根据mode处理结果渲染到哪里;
							// switch(this.mode){
							// 	case "date":
							// 		break;
							// }
							this.resultInfo={...val};
							console.log(this.resultInfo)
							this.dladd_address=this.resultInfo.result
							this.dladd_sheng=this.resultInfo.checkValue[0]
							this.dladd_shi=this.resultInfo.checkValue[1]
							this.dladd_qu=this.resultInfo.checkValue[2]
							this.dladd_diqustr=this.resultInfo.checkArr[0]+" "+this.resultInfo.checkArr[1]+" "+this.resultInfo.checkArr[2]
						this.areaCode = [this.dladd_sheng,this.dladd_shi,this.dladd_qu];
						}
					
						
		},
		
	}
</script>

<style>
	
	.tui-addr-box {
		padding: 20rpx 0;
	}

	.tui-line-cell {
		width: 100%;
		padding: 24rpx 30rpx;
		box-sizing: border-box;
		display: flex;
		align-items: center;
	}

	.tui-title {
		width: 180rpx;
		font-size: 28rpx;
	}

	.tui-title-city-text {
		width: 180rpx;
		height: 40rpx;
		display: block;
		line-height: 46rpx;
	}

	.tui-input {
		width: 500rpx;
	}

	.tui-input-city {
		flex: 1;
		height: 40rpx;
		font-size: 28rpx;
		padding-right: 30rpx;
	}

	.tui-phcolor {
		color: #ccc;
		font-size: 28rpx;
	}
	.tui-cell-title{
		font-size: 28rpx;
	}
	.tui-addr-label {
		margin-left: 70rpx;
	}

	.tui-label-item {
		width: 76rpx;
		height: 40rpx;
		border: 1rpx solid rgb(136, 136, 136);
		border-radius: 6rpx;
		font-size: 26rpx;
		text-align: center;
		line-height: 40rpx;
		margin-right: 20rpx;
		display: inline-block;
		transform: scale(0.9);
	}
	.tui-label-active{
		background: #E41F19;
		border-color:#E41F19;
		color: #fff;
	}
	.tui-swipe-cell {
		width: 100%;
		display: flex;
		justify-content: space-between;
		align-items: center;
		background: #fff;
		padding: 10rpx 24rpx;
		border-radius: 6rpx;
		overflow: hidden;
		font-size: 28rpx;
	}

	.tui-switch-small {
		transform: scale(0.8);
		transform-origin: 100% center;
	}

	/* #ifndef H5 */
	.tui-switch-small .wx-switch-input {
		margin: 0 !important;
	}

	/* #endif */

	/* #ifdef H5 */
	>>>uni-switch .uni-switch-input {
		margin-right: 0 !important;
	}

	/* #endif */

	.tui-addr-save {
		padding: 24rpx;
		margin-top: 100rpx;
	}

	.tui-del {
		padding: 24rpx;
	}
	/* picker start*/
	
	.tui-mask-screen {
		position: fixed;
		top: 0;
		left: 0;
		right: 0;
		bottom: 0;
		background: rgba(0, 0, 0, 0.6);
		z-index: 99996;
		transition: all 0.3s ease-in-out;
		opacity: 0;
		visibility: hidden;
	}
	
	.tui-mask-show {
		opacity: 1;
		visibility: visible;
	}
	
	.tui-picker-box {
		width: 100%;
		position: fixed;
		left: 0;
		right: 0;
		bottom: 0;
		z-index: 99999;
		visibility: hidden;
		transform: translate3d(0, 100%, 0);
		transform-origin: center;
		transition: all 0.3s ease-in-out;
		min-height: 20rpx;
		background: #fff;
	}
	
	.tui-pickerbox-show {
		transform: translate3d(0, 0, 0);
		visibility: visible;
	}
	
	.picker-header {
		width: 100%;
		height: 90upx;
		padding: 0 46upx;
		display: flex;
		justify-content: space-between;
		align-items: center;
		box-sizing: border-box;
		font-size: 32upx;
		background: #fff;
	}
	
	.list-item::after {
		left: 0;
	}
	
	.btn-cancle {
		padding: 20upx;
		color: #888;
	}
	
	.btn-sure {
		padding: 20upx;
		color: #5677fc;
	}
	
	.picker-view {
		width: 100%;
		height: 260px;
	}
	
	.item {
		line-height: 50px;
		text-align: center;
	}
	.btn-save{ background: #90A0E4 !important;}
	
	/* picker end*/
</style>
