<template>
	<view class="padding-lf30 padding-t30">
		<w-picker mode="region" :areaCode="areaCode" :hideArea="false" @confirm="onConfirm" ref="region" :timeout="true"></w-picker>
		<form @submit="" @reset="" :report-submit="true">
			<view class="label color9">
				填写收货人信息
			</view>
			<view class="bgf9">
				<input type="text" value="" v-model="dladd_contact" placeholder="请输入收货人姓名" class="fon28  bin-txt" />
				<input type="number" value="" v-model="dladd_tel" placeholder="请输入收货人联系电话" class="fon28  bin-txt" />
			</view>

			<view class="label color9 flex flex-just-between">
				<view class="">
					设置收货地址
				</view>
				<view class="color-org dingwei">
					定位
				</view>
			</view>
			<view class="bgf9">
				<!-- <view class="tui-title"><text class="tui-title-city-text">所在城市</text></view> -->
				<view class="tui-cell-arrow positionr">
					<input @tap="toggleTab('region')" placeholder-class="tui-phcolor" v-model="dladd_diqustr" class="fon28  bin-txt"
					 disabled name="city" placeholder="所在地区" maxlength="50" type="text" />
				</view>
				<input type="text" value="" v-model="dladd_address" placeholder="请输入详细地址" class="fon28  bin-txt" />
			</view>

			<view class="  flex flex-al-between flex-just-between">
				<view class="">
					<view class=" fon30">
						设置为默认地址
					</view>
					<view class="color9">
						（提醒每次下单默认推荐使用该地址）
					</view>
				</view>
				<view class="uni-list-cell uni-list-cell-pd">
					<!-- <view class="uni-list-cell-db">关闭</view> -->
					<switch :checked="dladd_default?true:false" @change="switchChange" color='#f9c276' style="transform: scale(0.5);" />
				</view>
			</view>
			<button @click="onSave" form-type="submit" class=" btns btns-tijiao colorf">确认</button>
			<button @click="onDelete"  v-if="false" class="btn-submit colorf">删除收货地址</button>

		</form>
	</view>
</template>

<script>
	const util = require('../../utils/util.js')
	import wPicker from "@/components/w-picker/w-picker.vue";
	export default {
		components: {
			
			wPicker,
		},
		data() {
			return {
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
		mounted() {
			if(this.dladd_id!='0'){
			//if(this.dladd_id=6){
				this.getData();
			}
		  },
		computed: {
		    // 计算属性
		    distr : function () {
					 return 1
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
				if(!util.isMobile(this.dladd_tel)) {
					this.tui.toast('请输入正确的手机号码');
					return
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
				if(this.dladd_default){
					uni.showModal({
					    title: '设置默认地址',
					    content: '每次下单将默认推荐使用该地址',
					    success: function (res) {
					        if (res.confirm) {
								
					            console.log('用户点击确定');
								
								_this.tui.request('/mine/addresssave',param).then(function(data){
									if(data.stat == 1){
										uni.navigateBack({
										    delta: 1
										});
									}
								})
					        } else if (res.cancel) {
					            console.log('用户点击取消');
					        }
					    }
					});
				}else{
					_this.tui.request('/mine/addresssave',param).then(function(data){
						if(data.stat == 1){
							uni.navigateBack({
							    delta: 1
							});
						}
					})
				}
				
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

<style lang="scss" scoped>
	page {
		background: #fff;
	}

	.bgf9 {
		background-color: #f9f9f9;
		border-radius: 10rpx;
		padding: 30rpx;
		margin-top: 30rpx;
		margin-bottom: 60rpx;
	}

	.btn-submit {
		width: 690rpx;
		line-height: 80rpx;
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

	.tui-cell-arrow:before {
		content: " ";
		height: 11px;
		width: 11px;
		border-width: 2px 2px 0 0;
		border-color: #b2b2b2;
		border-style: solid;
		-webkit-transform: matrix(0.5, 0.5, -0.5, 0.5, 0, 0);
		transform: matrix(0.5, 0.5, -0.5, 0.5, 0, 0);
		position: absolute;
		top: 50%;
		margin-top: -7px;
		right: 0;
	}
	.dingwei{ background: url(~@/static/images/dingwei.png) no-repeat left center; background-size: 27rpx; padding-left:35rpx;}
</style>
