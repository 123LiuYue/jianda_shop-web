<template>
	<view class="home">
		<swiper indicator-dots autoplay>
			<swiper-item v-for="item in swipers" :key="item.pictureId">
				<image :src="item.pictureSite"></image>
			</swiper-item>
		</swiper>
		<!-- 导航区域 -->
		<view class="nav">	
			<view class="nav_item" v-for="(item,index) in navs" :key="index" @click="navItemClick(item.path)">
				<view class="nav_img">
					<image :src="item.image"></image>
				</view>
				<text>{{item.titile}}</text>
			</view>
		</view>
		<!-- 推荐商品区域 --> 
		<view class="hot_goods">
			<view class="tit">推荐商品</view>
			<goods-list @goodsItemClick="goGoodsDetail" :goods="goods"></goods-list>
		</view>
	</view>
</template>

<script>
	import goodsList from '../../components/goods-list/goods-list.vue'	//导入自定义组件
	export default {
		data() {
			return {
				swipers: [],
				goods:[],
				navs:[
					{	
						image:'../../static/font/commodity.png',
						titile:'建达超市',
						path:'/pages/goods/goods'
					},
					{
						image:'../../static/font/AboutUs.png',
						titile:'联系我们',
						path:'/pages/contact/contact'
					},
					{
						image:'../../static/font/img.png',
						titile:'社区图片',
						path:'/pages/pics/pics'
					},
					{
						image:'../../static/font/video.png',
						titile:'学习视频',
						path:'/pages/views/views'
					}
				]
			}
		},
		onLoad() {
			this.getSwipers()
			this.getHotGoods()
		},
		components:{"goodsList":goodsList},
		methods: {
			//获取轮播图的数据
			async getSwipers() {
				const res = await this.$myRequest({
					url: '/picture/findAll'
				})
				this.swipers = res.data
				console.log(res)
			},
			//获取热门商品列表数据
			async getHotGoods(){
				const res = await this.$myRequest({
						url:'/commodity/findAll'  
				})
				this.goods = res.data
			},
			//导航点击的出来函数
			navItemClick(url){
				uni.navigateTo({
					url
				})
			},
			//导航到商品详情页
			goGoodsDetail (commodityId) {
				uni.navigateTo({
						url: '/pages/goods-detail/goods-detail?commodityId='+commodityId
				})
			}
		}
	}
</script>

<style lang="scss">
	.home {
		swiper {
			width: 750rpx;
			height: 380rpx;

			image {
				width: 100%;
				height: 100%;
			}
		}


		.nav {
			display: flex;
			margin-top: 15rpx;
			.nav_item {
				float: left;
				width: 25%;
				text-align: center; //文字居中

				.nav_img {
					width: 120rpx;
					height: 120rpx;
					background: $shop-color;
					border-radius: 60rpx; //设置成圆形
					margin: 10rpx auto; //居中
					line-height: 120rpx; //行高

					#h3 {
						width: 60rpx; //图片的宽
						height: 60rpx; //图片的高
						margin: 28rpx auto; //居中
					}

					image {
						margin: 25rpx auto; //居中
						width: 67rpx; //图片的宽
						height: 67rpx; //图片的高
						color: #FFFFFF;
					}
				}

				text {
					font-size: 30rpx;
				}
			}
		}

		.hot_goods {
			background: #eee;
			overflow: hidden;
			margin-top: 20rpx; //上边距 

			.tit {
				height: 50px;
				line-height: 50px;
				color: $shop-color;
				text-align: center; //文字居中
				letter-spacing: 20px; //间距
				background: #FFFFFF;
				margin: 7rpx 0; //间距
			}
		}
	}
</style>
