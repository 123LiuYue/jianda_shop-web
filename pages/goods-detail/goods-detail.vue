<template>
	<view class="goods_detail">
		<swiper indicator-dots>
			<swiper-item v-for="item in swipers" :key="item.commodityId">
				<image :src="item.img1"></image>
			</swiper-item>
		</swiper>
		<view class="box1">
			<view class="price">
				<text>￥{{info.price}}</text>
				<text>￥{{info.formerPrice}}</text>
			</view>
			<view class="goods_name">{{info.commodityName}}</view>
		</view>
		<view class="line"></view>
		<view class="box2">
			<view>商品编号：{{info.number}}</view>
			<view>库存：{{info.inventory}}</view>
		</view>
		<view class="line"></view>
		<view class="box3">
			<view class="tit">详情介绍</view>
			<view class="content">
				<rich-text :nodes="info.parameter"></rich-text>
			</view>
		</view>
		<view class="goods_nav">
			<uni-goods-nav :fill="true" :options="options" :buttonGroup="buttonGroup" @click="onClick" @buttonClick="buttonClick" />
		</view>
	</view>
</template>

<script>
	//导入组件
	import uniGoodsNav from '@/components/uni-goods-nav/uni-goods-nav.vue'
	export default {
		data() {
			return {
				//定义id
				id: 0,
				//定义数组
				swipers: [],
				info: {},
				content: '',
				//组件数据
				options: [{
					icon: 'headphones',
					text: '客服'
				}, {
					icon: 'shop',
					text: '店铺',
					info: 6,
					infoBackgroundColor: '#007aff',
					infoColor: "red"
				}, {
					icon: 'cart',
					text: '购物车',
					info: 2
				}],
				buttonGroup: [{
						text: '加入购物车',
						backgroundColor: '#ff0000',
						color: '#fff'
					},
					{
						text: '立即购买',
						backgroundColor: '#ffa200',
						color: '#fff'
					}
				]
			}
		},
		//事件函数
		methods: {
			//组件方法
			onClick (e) {
			        uni.showToast({
			          title: `点击${e.content.text}`,
			          icon: 'none'
			        })
			      },
			      buttonClick (e) {
			        console.log(e)
			        this.options[2].info++
			      },
			async getSwipers() {
				const res = await this.$myRequest({
					url: '/detailTake/findByIdAll?commodityId=' + this.id
				})
				this.swipers = res.data
				console.log(res)
			},
			async getDetailInfo() {
				const res = await this.$myRequest({
					url: '/detailedDescription/findByIdAll?commodityId=' + this.id
				})
				this.info = res.data
			}
		},
		onLoad(options) {
			//将获取到的id放入到定义的id中
			this.id = options.commodityId
			//调用getSwipers方法
			this.getSwipers()
			//调用getDetailInfo
			this.getDetailInfo()
		},
		//注册组件
		components: {
			uniGoodsNav
		}
	}
</script>

<style lang="scss">
	.goods_detail {
		swiper {
			height: 700rpx;

			image {
				width: 100%;
				height: 100%;
			}
		}

		.box1 {
			padding: 10px;

			.price {
				font-size: 35rpx;
				color: $shop-color;
				line-height: 80rpx;

				text:nth-child(2) {
					color: #C0C0C0;
					font-size: 28rpx;
					text-decoration: line-through;
					margin-left: 20rpx;
				}
			}

			.goods_name {
				font-size: 32rpx;
				line-height: 60rpx;
			}
		}

		.box2 {
			padding: 0 10px;
			font-size: 30rpx;
			line-height: 60rpx;
		}

		.box3 {
			padding-bottom: 50rpx;
			.tit {
				font-size: 32rpx;
				padding-left: 10rpx;
				border-bottom: 1px solid #eee;
				line-height: 70rpx;
			}

			.content {
				padding: 10rpx;
				font-size: 25rpx;
			}
		}
	}
.goods_nav{
	position: fixed;
	bottom: 0;
	width: 100%;
}

	.line {
		height: 10rpx;
		width: 750rpx;
		background: #eee;
	}
</style>
