<template>
	<view class="pics">
		<scroll-view class="left" scroll-y>
			<view :class="active===index?'active':''" v-for="(item,index) in cates" @click="leftClickHandle(index,item.titleId)">{{item.titleName}}</view>
		</scroll-view>
		<scroll-view class="right" scroll-y>
			<view class="item" v-for="item in secondData" :kye="item.titleId">
				<image @click="previewImg(item.img)" :src="item.img"></image>
				<text>{{item.content}}</text>
				<text v-if="secondData.length === 0">暂无数据</text>
			</view>
			
		</scroll-view>
	</view>
</template>

<script>
	export default {
		data(){
			return {
				cates:[],
				active:0,
				secondData:[]
			}
		},
		methods:{  //事件函数
			async getPicsCate(){
				const res = await this.$myRequest({
					url:'/title/finAll'
				})
				this.cates = res.data
				this.leftClickHandle(0,this.cates[0].titleId)
			},
			async leftClickHandle(index,titleId){
				//点击改变颜色
				this.active = index
				//获取右侧数据	
				const res = await this.$myRequest({
					url:'/content/findByIdAll?titleId='+titleId
				})
				this.secondData[0] = res.data 
				console.log(res.data)
			},
			previewImg(current){
				const urls = this.secondData.map(item =>{
					return item.img
				})
				
				uni.previewImage({
					current,
					urls
				}) 
				
			}
		},
		onLoad() {
			this.getPicsCate()
		}
	}
</script>

<style lang="scss">
	page{
		height: 100%;
	}
	.pics{
		height: 100%;
		display: flex;
		.left{
			width: 200rpx;
			height: 100%;
			border-right: 1px solid #eee;
			view{
				height: 60px;
				line-height: 60px;
				border-top: 1px solid #eee;
				color: #333333;
				text-align: center;//居中
				font-size: 30rpx;//字体大小
			}
			.active{
				background: $shop-color;
				color: #FFFFFF;
			}
		}
		.right{
			width: 520rpx;
			height: 100%;
			margin: 10rpx auto;
			.item{
				image{
					width: 532rpx;
					background: #007AFF;
					height: 532rpx;
					border-radius: 5px; //图片圆角
				}
				text{
					font-size: 30rpx;
					line-height: 20rpx;
				}
			}
		}
	}
</style>
