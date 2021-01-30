<template>
	<view>
		<!-- swiper
		 1.自动轮播autoplay
		 2.指示器 indicator-dots
		 3.衔接轮播 circular
		 
		 4.swiper
		 默认高度为 150px
		 5.image
		 默认的高度 320px => 基本样式中 重置了 100%
		 默认的高度 240px
		 6.计算图片的宽度和高度的比例
		 7.把图片的比例也写道swiper标签样式
		 8.swiper宽高
		 -->
		 <!-- 轮播图开始 -->
		 <view class="album_swiper">
			 <swiper class="album_swiper_box">
				 <swiper-item class="album_swiper_item" v-for="item in bannerlist" :key="item.id">
					 <image class="album_swiper_image" :src="item.thumb" mode="widthFix"></image>
				 </swiper-item>
			 </swiper>
		 </view>
		 <!-- 轮播图结束 -->
		 <view class="album_list">
			 <view class="album_item" v-for="item in albumlist" :key="item.id">
				 <view  class="album_item_img" >
					<image class="album_item_img" :src="item.cover" ></image>
				 </view>
				 <view class="album_item_info">
					 <view class="album_item_title">{{item.name}}</view>
					 <view class="album_item_desc">{{item.desc}}</view>
					 <view class="btn">
						<view class="btn_txt">+ 关注</view>
					 </view>
				 </view>
			 </view>
		 </view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				pramas:{
					limit:30,
					order:"new",
					skip:0
				},
				// 轮播图列表
				bannerlist:[],
				albumlist:[]
			}
		},
		 mounted() {
		 	this.getList();
		 },
		methods: {
			// 获取数据
			getList(){
				this.request({
					url:"http://service.picasso.adesk.com/v1/wallpaper/album",
					data: this.pramas
				})
				.then(res => {
					console.log(res)
					// 轮播图列表
					this.bannerlist = res.res.banner
					// 列表数据
					this.albumlist = res.res.album
					console.log(this.albumlist)
				})
			},
		}
	}
</script>

<style lang="scss" scoped>
	.album_swiper{
		
		.album_swiper_box{
			 height:335rpx;
			.album_swiper_item{
				.album_swiper_image{
					width: 100%;
					display: block;
					vertical-align: center;
				}
			}
		}
	}
	.album_list{
		padding:2rpx;
	    .album_item{
			padding: 5rpx;
			display:flex;
			border-bottom: 1rpx solid #666;
			.album_item_img{
				width:200rpx;
				height:200rpx;	
			}
			.album_item_info{
				margin-left:15rpx;
				width:100%;
				overflow: hidden;
				.album_item_title{
					font-size:30rpx;
					font-weight: 700;
				}
				.album_item_desc{
					// width:100%;
					font-size:24rpx;
					text-overflow: ellipsis;
					white-space: nowrap;
					overflow: hidden;
				}
				.btn{
					display: flex;
					justify-content: flex-end;
					width:100%;
					margin-top: 30rpx;
					.btn_txt{
						width:80rpx;
						height:35rpx;
						border:2rpx solid $color;
						font-size:20rpx;
						font-weight:600;
						color:$color;
						text-align: center;
						line-height: 35rpx;
					}
					
				}
			}
		}
	}
</style>
