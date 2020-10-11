<template>
	<view class="goods-list">
		<goodsList @goodsItemClick="goGoodsDetail" :goods="goods"></goodsList>
		<view class="isOver" v-if="flag">-----我是有底线的-----</view>
	</view>
</template>
<script>
	import goodsList from '../../components/goods-list/goods-list.vue'
	export default{
		data(){
			return{
				goods:[],
				pageindex:1,
				flag:false
			}
		},
		components:{"goodsList":goodsList},
		methods:{
			//获取商品列表的数据
			async getGoodsList(callBack){
				const res = await this.$myRequest({
					url:'/commodity/findAll'
				})
				this.goods = [...this.goods, ...res.data]
				callBack && callBack()
			},
			//导航到商品详情页
			goGoodsDetail (commodityId) {
				uni.navigateTo({
					url:'/pages/goods-detail/goods-detail?commodityId='+commodityId
				})
				
			}
		},
		//生命周期函数
		onLoad() {
			this.getGoodsList()
		},
		onReachBottom(){ //触底触发
			console.log(this.goods.length)
			if(this.goods.length<this.pageindex*10) return this.flag = true
			console.log('触底了')
			this.getGoodsList()
		},
		onPullDownRefresh(){ //监听下拉刷新
			console.log('下拉刷新')
			this.pageindex =1
			this.goods = []
			this.flag = false
			setTimeout(()=>{
				this.getGoodsList(()=>{
					uni.stopPullDownRefresh()
				})
			},1000)
		}
	}
</script>

<style lang="scss">
	.goods-list{
		background: #EEE;
	}
	.isOver{
		width: 100%;
		height: 50px;
		line-height: 50px;
		text-align: center;
		font-size: 28rpx;
	}
</style>
