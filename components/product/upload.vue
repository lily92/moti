<template>
	<view>
		<tui-list-cell  :hover="false">
			<view class="tui-padding tui-flex">
				<view v-if="name">{{name}}</view>
				<view class="tui-upload-box">
				  <view class="tui-upload-item" v-for="(item,index) in files" :key="index">
				    <image :src="item" class='tui-upload-img' @tap="previewImage" mode="aspectFill" :id="item"></image>
				    <tui-icon :color="close_color" :size="24" name="close-fill" class="tui-upload-del" :index="index" @click="deleteImage"></tui-icon>
				  </view>
				  
				  <view class="tui-upload-item tui-upload-add" v-if="files.length < limit" hover-class="tui-opcity" :hover-stay-time="150" @tap="chooseImage">
				    <text>+</text>
				    
				  </view>
				 <!-- <text style="font-size: 8rpx;">(可上传多张图片)</text> -->
				</view>
			</view>
		</tui-list-cell>
	</view>
		
	
</template>

<script>
	import tuiIcon from "@/components/icon/icon"
	import tuiTabs from "@/components/tui-tabs/tui-tabs"
	import tuiListCell from "@/components/list-cell/list-cell"
	export default {
		components: {
			tuiListCell,
			tuiTabs,
			tuiIcon,
		},
		name: "myUpload",
		props: {
			
			name: {//名称
				type: String,
				default: "上传收款码"
			},
			close_color: {//关闭按钮颜色
				type: String,
				default: "#ed3f14"
			},
			ttamp: {//上传时间戳
				type: Number,
				default: 0
			},
			sture: {//上传校验串
				type: String,
				default: ""
			},
			limit: {//数量限制
				type: Number,
				default: 1
			},
			files: {//图片列表
				type: Array,
				default: function() {
					return []
				}
			},
			
		},
		data() {
			return {
				
			};
		},
		methods: {
			chooseImage: function (e) {
								let that = this;
								if (that.files.length >= that.limit) {
									that.tui.toast("最多上传"+that.limit+"张图片");
									return
								}
								console.log(that.files)
								uni.chooseImage({
									count: 1, //默认9
									sizeType: ['original', 'compressed'], //可以指定是原图还是压缩图，默认二者都有
									sourceType: ['album'], //从相册选择
								    success: (chooseImageRes) => {
										//console.log(chooseImageRes)
										//that.files=that.files.concat(chooseImageRes.tempFilePaths)
								        const tempFilePaths = chooseImageRes.tempFilePaths;
								        const appArr = getApp().globalData;
										
										that.tui.uploadFile(tempFilePaths[0],that.ttamp,that.sture).then(function(data) {
											
											if (data.stat == 1) {
												that.add(chooseImageRes.tempFilePaths,data.savename)
											}
										});
								    }
								});
							
							},
							previewImage: function (e) {
								uni.previewImage({
									current: e.currentTarget.id, // 当前显示图片的http链接
									urls: this.files // 需要预览的图片http链接列表
								})
							},
							deleteImage: function (e) {
								const index = e.index;
								this.del(index)
								// this.files.splice(index, 1);
								// this.file_name.splice(index, 1);
								
							},
							add(index,index1) {
								this.$emit('add', index,index1)
							},
							del(index) {
								this.$emit('del', index)
							},
		},
		
		mounted() {
			
		},
	}
</script>

<style>
	@import '../../static/style/thorui.css';
	.tui-padding {
		box-sizing: border-box;
	}
	.tui-flex {
		width: 100%;
		display: flex;
		align-items: center;
		justify-content: space-between;
		font-size: 26rpx;
	}
	/deep/.tui-upload-item  {
		margin-right:26rpx!important;
	}
	.tui-list-cell{ padding-left: 0 !important; padding-right: 0 !important;}
	.tui-upload-item{ margin-right: 22rpx !important;}
	.tui-list-cell::after{border-bottom:0 !important}
	.tui-upload-img{ width:148rpx  !important ; height: 148rpx !important;}
</style>
