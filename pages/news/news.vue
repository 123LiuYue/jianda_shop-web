<template>
	<view class="news">
		<news-item @itemClick="goDetail" :list="newsList"></news-item>
	</view>
</template>

<script>
	//导入组件
	import newsItem from '../../components/news-item/news-item.vue'
	export default{
		data(){
			return{
				newsList:[]
			}
		},
		methods:{ //事件函数
			async getNews(){
				const res = await this.$myRequest({
					url:'/consult/findAll'
				})
				this.newsList = res.data
			},
			goDetail (consultId){ //跳转页面的方法
				uni.navigateTo({
					url:'/pages/news-detail/news-detail?consultId='+consultId
				})
			}
		},
		//注册
		components:{"news-item":newsItem},
		
		onLoad() {
			this.getNews()
		}
	}
	
</script>

<style lang="scss">
	.news{
		
	}
	
</style>
