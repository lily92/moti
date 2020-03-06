<template>
	<view>
		<tui-list-cell :hover="false" :lineLeft="false">
			<view class="tui-goods-title">
				<view>订单号：{{model.od_orderid}}</view>
				<view class="tui-order-status">{{model.od_state_str}}</view>
			</view>
		</tui-list-cell>
		<block v-for="(item,index) in model.oddtinfo" :key="index">
			<tui-list-cell padding="0" @click="proDetail(item.oddt_proid)">
				<view class="tui-goods-item">
					<image :src="item.oddt_pic_link" class="tui-goods-img"></image>
					<view class="tui-goods-center">
						<view class="tui-goods-name">{{item.oddt_proname}}</view>
						<view class="tui-goods-attr">{{item.oddt_psd_str}}</view>
					</view>
					<view class="tui-price-right">
						<view>￥{{item.oddt_dlprice}}</view>
						<view>x{{item.oddt_qty}}</view>
					</view>
				</view>
			</tui-list-cell>
		</block>
		<tui-list-cell v-if="model.od_cdid_str" :hover="false" :last="true">
			<view class="tui-goods-title">
				<view>
					使用优惠券
					</view>
			</view>
			<view class="tui-goods-price">
				<view style="color: red;">{{model.od_cdid_str}}</view>
				
			</view>
		</tui-list-cell>
		<tui-list-cell :hover="false" :last="true">
			<view class="tui-goods-title">
				<view>
					<tui-icon name="time" :size="20" ></tui-icon>
					{{model.od_addtime}}
					</view>
			</view>
			<view class="tui-goods-price">
				<view>共{{model.total_num}}件商品 合计：</view>
				<view class="tui-size-24">￥</view>
				<view class="tui-price-large">{{model.od_total}}</view>
				<!-- <view class="tui-size-24">.00</view> -->
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
		name: "tuiOrder",
		props: {
			//数量
			// productList: {
			// 	type: Array,
			// 	default: function() {
			// 		return []
			// 	}
			// },
			model: {
				type: Object,
				default: function() {
					return {}
				}
			},
		},
		data() {
			return {
				
			};
		},
		methods: {
			detail(index) {
				this.$emit('detail', index)
			},
			proDetail(index) {
				this.$emit('proDetail', index)
			},
		},
		
		mounted() {
			
		},
	}
</script>

<style>
	.tui-order-item {
		margin-top: 20rpx;
		border-radius: 10rpx;
		overflow: hidden;
	}
	
	.tui-goods-title {
		width: 100%;
		font-size: 28rpx;
		display: flex;
		align-items: center;
		justify-content: space-between;
	}
	
	.tui-order-status {
		color: #888;
		font-size: 26rpx;
	}
	
	.tui-goods-item {
		width: 100%;
		padding: 20rpx 30rpx;
		box-sizing: border-box;
		display: flex;
		justify-content: space-between;
	}
	
	.tui-goods-img {
		width: 180rpx;
		height: 180rpx;
		display: block;
		flex-shrink: 0;
	}
	
	.tui-goods-center {
		flex: 1;
		padding: 20rpx 8rpx;
		box-sizing: border-box;
	}
	
	.tui-goods-name {
		max-width: 310rpx;
		word-break: break-all;
		overflow: hidden;
		text-overflow: ellipsis;
		display: -webkit-box;
		-webkit-box-orient: vertical;
		-webkit-line-clamp: 2;
		font-size: 26rpx;
		line-height: 32rpx;
	}
	
	.tui-goods-attr {
		font-size: 22rpx;
		color: #888888;
		line-height: 32rpx;
		padding-top: 20rpx;
		word-break: break-all;
		overflow: hidden;
		text-overflow: ellipsis;
		display: -webkit-box;
		-webkit-box-orient: vertical;
		-webkit-line-clamp: 2;
	}
	
	.tui-price-right {
		text-align: right;
		font-size: 24rpx;
		color: #888888;
		line-height: 30rpx;
		padding-top: 20rpx;
	}
	
	.tui-color-red {
		color: #E41F19;
		padding-right: 30rpx;
	}
	
	.tui-goods-price {
		width: 100%;
		display: flex;
		align-items: flex-end;
		justify-content: flex-end;
		font-size: 24rpx;
	}
	
	.tui-size-24 {
		font-size: 24rpx;
		line-height: 24rpx;
	}
	
	.tui-price-large {
		font-size: 32rpx;
		line-height: 30rpx;
		font-weight: 500;
	}
	
</style>
