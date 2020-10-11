<template>
	<view>
		<view class="news_item" @click="navigator(item.consultId)" v-for="item in list" :key="item.consultId">
			<image :src="item.consultImg"></image>
			<view class="right">
				<view class="tit">
					{{item.journalism}}
				</view>
				<view class="info">
					<text>发表时间：{{item.time}}</text>
					<text>浏览：{{item.browse}}</text>
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		props:['list'],
		//过滤器
		filters:{
			formatData (data){
				const nDate  = new Date(data)
				const year = nDate.getFullYear() //获取年
				const month = nDate.getMonth().toString().padStart(2,0) //获取月
				const day = nDate.getDay().toString().padStart(2,0) //获取日
				return year+'-'+month+'-'+day
			}
		},
		methods:{ //事件函数
			navigator (consultId) { //点击跳转页面
				this.$emit('itemClick',consultId)
			}
		}
	}
	
</script>

<style lang="scss">
	.news_item{
		display: flex;
		padding: 10rpx 20rpx;
		border-bottom: 1px solid $shop-color;
		image{
			max-width: 200rpx;
			min-width: 200rpx;
			height: 150rpx;
		}
		.right{
			margin-left: 15rpx;
			display: flex;
			flex-direction: column;
			justify-content: space-between; //主轴对应方式
			.tit{
				font-size: 30rpx;
			}
			.info{
				font-size: 24rpx;
				text:nth-child(2){
					margin-left: 30rpx;
				}
			}
		}
	}
</style>
