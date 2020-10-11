<template>
	<view class="goods_list">
		<view class="goods_item" v-for="item in goods" :key="item.commodityId" @click="navigator(item.commodityId)">
			<image :src="item.commodityImg"></image>
			<view class="price">
				<text>￥{{item.price}}</text>
				<text>￥{{item.formerPrice}}</text>
			</view>
			<view class="name">
				{{item.commodityName}}
			</view>
		</view>
		
	</view>
</template>

<script>
	export default{
		props:['goods'],
		methods:{ //事件函数
			navigator(commodityId){
				//首页商品列表跳转到商品详情
				this.$emit('goodsItemClick',commodityId)
			}
		}
	}
	
</script>

<style lang="scss">
	.goods_list{
		padding: 0 15rpx; 
		display: flex; 	//在一行显示
		flex-wrap: wrap;	//换行
		justify-content: space-between;  //左右分离
		.goods_item{
			background: #FFFFFF;
			margin: 8rpx 0;
			width: 355rpx;
			padding: 15rpx;
			box-sizing: border-box;
			image{
				width: 80%;
				height: 150px;
				display: block;
				margin: 0 auto;	//居中
			}
			.price{
				color: $shop-color;
				font-size: 34rpx;
				margin: 10rpx 0 5rpx 0;
				text:nth-child(2){		//选择第二个text标签
					color: #C0C0C0;
					font-size: 28rpx;
					margin-left: 17rpx;
					text-decoration: line-through; //中位线
				}
			}
			.name{
				font-size: 28rpx;
				line-height: 50rpx;
				padding-bottom: 15rpx;  //下边距
				padding-top: 10rpx;		//上边距
			}
		}
	}
</style>
