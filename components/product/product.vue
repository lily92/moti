<template>
	
		<view class="tui-product-list">
			<view class="tui-product-container">
				<block v-for="(item,index) in productList" :key="index" v-if="(index+1)%2!=0">
					<!--商品列表-->
					<view class="tui-pro-item" hover-class="hover" :hover-start-time="150" @tap="detail(item.pro_id)">
						<image :src="item.pic_link" class="tui-pro-img" mode="widthFix" />
						<view class="tui-pro-content">
							<view class="tui-pro-tit">{{item.pro_name}}</view>
							<view>
								<view class="tui-pro-price">
									<text class="tui-sale-price">￥{{item.pro_dlprice}}</text>
									<text v-if="item.pro_dlprice<item.pro_price" class="tui-factory-price">￥{{item.pro_price}}</text>
								</view>
								<view class="tui-pro-pay">{{item.pro_sale}}人付款</view>
							</view>
						</view>
					</view>
					<!--商品列表-->
					<!-- <template is="productItem" data="{{item,index:index}}" /> -->
				</block>
			</view>
			<view class="tui-product-container">
				<block v-for="(item,index) in productList" :key="index" v-if="(index+1)%2==0">
					<!--商品列表-->
					<view class="tui-pro-item" hover-class="hover" :hover-start-time="150" @tap="detail(item.pro_id)">
						<image :src="item.pic_link" class="tui-pro-img" mode="widthFix" />
						<view class="tui-pro-content">
							<view class="tui-pro-tit">{{item.pro_name}}</view>
							<view>
								<view class="tui-pro-price">
									<text class="tui-sale-price">￥{{item.pro_price}}</text>
									<text class="tui-factory-price">￥{{item.pro_price}}</text>
								</view>
								<view class="tui-pro-pay">{{item.pro_sale}}人付款</view>
							</view>
						</view>
					</view>
					<!--商品列表-->
					<!-- <template is="productItem" data="{{item,index:index}}" /> -->
				</block>
			</view>
		</view>
	
</template>

<script>
	export default {
		name: "tuiProduct",
		props: {
			//数量
			productList: {
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
			detail(index) {
				this.$emit('detail', index)
			},
		},
		
		mounted() {
			
		},
	}
</script>

<style>
	.tui-product-list {
		display: flex;
		justify-content: space-between;
		flex-direction: row;
		flex-wrap: wrap;
		box-sizing: border-box;
		/* padding-top: 20rpx; */
	}
	
	.tui-product-container {
		flex: 1;
		margin-right: 2%;
	}
	
	.tui-product-container:last-child {
		margin-right: 0;
	}
	
	.tui-pro-item {
		width: 100%;
		margin-bottom: 4%;
		background: #fff;
		box-sizing: border-box;
		border-radius: 12rpx;
		overflow: hidden;
	}
	
	.tui-pro-img {
		width: 100%;
		display: block;
	}
	
	.tui-pro-content {
		display: flex;
		flex-direction: column;
		justify-content: space-between;
		box-sizing: border-box;
		padding: 20rpx;
	}
	
	.tui-pro-tit {
		color: #2e2e2e;
		font-size: 26rpx;
		word-break: break-all;
		overflow: hidden;
		text-overflow: ellipsis;
		display: -webkit-box;
		-webkit-box-orient: vertical;
		-webkit-line-clamp: 2;
	}
	
	.tui-pro-price {
		padding-top: 18rpx;
	}
	
	.tui-sale-price {
		font-size: 34rpx;
		font-weight: 500;
		color: #e41f19;
	}
	
	.tui-factory-price {
		font-size: 24rpx;
		color: #a0a0a0;
		text-decoration: line-through;
		padding-left: 12rpx;
	}
	
	.tui-pro-pay {
		padding-top: 10rpx;
		font-size: 24rpx;
		color: #656565;
	}
</style>
