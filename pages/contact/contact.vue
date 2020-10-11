<template>
	<view class="contact">
		<image class="img" src="../../static/contact/gywmban.jpg"></image>
		<view class="info">
			<view @click="phone">联系电话：400-123-3232 ( 点击拨打 )</view>
			<view>联系地址：陕西省西安市新城区环城北路西铁公寓</view>
			<!-- 地图组件 -->
			<map class="map" :markers="markers"></map> 
		</view>
	</view>
</template>

<script>
	export default{
		data(){
			return{
				
				markers:[
					{
						longitude:34.2834940000,
						latitude:108.9691220000,
						iconPath:'../../static/jiandalogo.jpg',
						width:30,
						height:30
					}
				]
			}
		},
		methods:{
			phone(){
				uni.makePhoneCall({
					phoneNumber:'400-123-3232'
				})
			}
		}
		
	}
</script>

<style lang="scss">
	.contact{
		.img{
			width: 750rpx;
			height: 320rpx;
		}
		.info{
			padding: 10rpx 20rpx;
			font-size: 30rpx;
			view{
				line-height: 70rpx;
				border-bottom: 1px solid #eee;
			}
		}
		.map{
			width: 750rpx;
			height: 750rpx;
		}
	}
</style>
