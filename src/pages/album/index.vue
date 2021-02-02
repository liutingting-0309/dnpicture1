<template>
	<view>
		<view class="album_banner">
			<image class="album_img" :src="album.cover" mode=""></image>
			<view class="album_info">
				<view class="album_title">{{album.name}}</view>
				<view class="gunzhubtn">关注专辑</view>
			</view>
		</view>
		<view class="album_desc">
			<view class="album_user">
				<image class="album_user_img" :src="album.user.avatar" mode=""></image>
				<text class="album_usrname">{{album.user.name}}</text>
			</view>
			<view class="album_desc_info">{{album.desc}}</view>
		</view>
		<view class="wallpaper">
			<view v-for="item in wallpaper" :key="item.id" class="wallpaper_imgs">
			<!-- <view 	class="wallpaper_imgs" v-for="item in 15"> -->
				<image class="wallpaper_img"  :src="item.thumb+item.rule.replace('$<Height>', 360)" mode=""></image>
				<!-- <image class="wallpaper_img"  src="http://img5.adesk.com/600fd1d1e7bce727de5ff0b4?imageView2/3/h/240" mode=""></image> -->
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				params:{
					limit:30,
					order:"new",
					skip:0,
					first:1
				},
				id:"",
				// 详情信息
				album:[],
				// 专辑列表
				wallpaper:[],
				hasMore:true
			}
		},
		onLoad(options){
			console.log(options)
			this.id = options.id;
			// this.id = "5e206ca6e7bce73981fb0752";
			this.getList();
		},
		onReachBottom(){
			if(this.hasMore){
				this.params.first = 0;
				this.params.skip += this.params.limit;
				this.getlist();	
			}else{
				uni.showToast({
					title:"到底了",
					icon:"none"
				})
			}
			
		},
		methods: {
			getList(){
				this.request({
					url:`http://service.picasso.adesk.com/v1/wallpaper/album/${this.id}/wallpaper`,
					data:this.params
				})
				.then(res =>{
					if(Object.keys(this.album).length === 0){
						this.album = res.res.album;
						console.log(res.res);
					}
					if(res.res.wallpaper.length === 0){
						this.hasMore = false;
						return;
					}
					this.wallpaper =  [...this.wallpaper,...res.res.wallpaper];
					console.log("wallpaper");
					console.log(this.wallpaper);
				})
			}
			
		}
	}
</script>

<style lang="scss" scoped>
.album_banner{
	position: relative;
	.album_img{
		width:100%;
		display:block;	
	}
	.album_info{
		position:absolute;
		width:100%;
		bottom:20rpx;
		display:flex;
		justify-content: space-between;
		color:#fff;
		.album_title{
			margin-left:20rpx;
		}
		.gunzhubtn{
			color:#fff;
			background-color: $color;
			font-size:20rpx;
			padding:10rpx;
			height:20rpx;
			line-height: 20rpx;
			text-align: center;
			margin-right:20rpx;
		}
	}
}
.album_desc{
	
	.album_user{
		padding:15rpx;
		display:flex;
		.album_user_img{
			width:50rpx;
			height:50rpx;
			display: block;
			vertical-align: center;	
		}
		.album_usrname{
			font-size:30rpx;
			font-weight:700;
			margin-left:10rpx;
		}
	}
	.album_desc_info{
		font-size:27rpx;
		padding:10rpx;
	}
}
.wallpaper{
	display:flex;
	flex-wrap: wrap;
	padding-left:3rpx;
	.wallpaper_imgs{
		width: 33%;
		margin: 0 0 2rpx 1rpx;
		.wallpaper_img{
			width:100%;
			height:207rpx;
			display: block;
		}
	}
}
</style>
