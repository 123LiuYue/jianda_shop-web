<template>
	<view class="news-detail" :key="detail.consultId">
		<text class="title">{{detail.headline}}</text>
		<view class="info">
			<text>发表时间：{{detail.time}}</text>
			<text>浏览：{{detail.browse}}</text>
		</view>
		<view class="contact">
			<rich-text :nodes="detail.details"></rich-text>
		</view>
	</view>
</template>

<script>
	export default{
		data(){
			return{
				//定义一个为零的id
				id:0,
				detail:{}
			}
		},
		methods:{ //事件函数
			async getNewsDetail () {
				const res = await this.$myRequest({
					url:'/consultant/findByIdAll?consultId='+this.id
				})
				console.log(res.data)
				this.detail = res.data
			}
		},
		//生命周期函数
		onLoad(options) {
			//将获取到的id放入定义的id
			this.id = options.consultId
			this.getNewsDetail()
			console.log(this.id)
		}
		
	}
</script>

<style lang="scss">
	.news-detail{
		font-size: 30rpx;
		padding: 0 20rpx;
		.title{
			text-align: center;
			width: 710rpx;
			display: block;
			margin: 20rpx 0;
		}
		.info{
			display: flex;
			justify-content: space-between;
		}
	}
		
</style>
