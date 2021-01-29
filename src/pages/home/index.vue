<template>
	<view>
		<view class="home_tab">
			<view class="home_tab_title">
				<view class="title_inner">
					<uni-segmented-control :current="current" :values="items.map(v=>v.title)" @clickItem="onClickItem" style-type="text" active-color="#d98cb8">
					</uni-segmented-control>
				</view>
				<view class="iconfont iconsearch">
					<!-- <img src="./static/icon/ordermanagement.png" alt="" style="width:30rpx;height:30rpx"> -->
				</view>
			</view>	
			<view class="home_tab_content">
				<view v-if="current === 0">
					<homeRecommend></homeRecommend>
				</view>	
				<view v-if="current === 1">
					<homeCategory></homeCategory>
				</view> 
				<view v-if="current === 2">
					<homeNew></homeNew>
				</view>
				<view v-if="current === 3">
					<homeAlbum></homeAlbum>
				</view>
			</view>
			<!-- {{Recommends[1].thumb}} -->
		</view>
		
	</view>
</template>

<script>
	
	import homeAlbum from "./home-album";
	import homeNew from "./home-new";
	import homeRecommend from "./home-recommend";
	import homeCategory from "./home-category";
	import {uniSegmentedControl} from "@dcloudio/uni-ui";
	
	export default {
		data() {
			return {
				items: [
					{title:'推荐'},
					{title:'分类'},
					{title:'最新'},
					{title:'专辑'}
					],
				// Recommends:[],
				current: 0
			}
		},
		// onLoad() {
			
		// 	console.log("ooo")
		// 	this.request({
				
		// 		// 接口不能用
		// 		// url:"http://157.122.54.189:9088/image/v3/homepage/vertical",
		// 		// 备用接口 可以看下面(部分图片没有 唉 再次认识到全栈的重要性~)
		// 		// 推荐: 
		// 		url: "http://service.picasso.adesk.com/v3/homepage/vertical"
		// 		// 专辑 http://service.picasso.adesk.com/v1/wallpaper/album
		// 		// 分类: http://service.picasso.adesk.com/v1/vertical/category
		// 		// 分类-最新-热门 http://service.picasso.adesk.com/v1/vertical/category/${id}/vertical
		// 		// 专辑 http://service.picasso.adesk.com/v1/wallpaper/album
		// 		// 专辑-详情 http://service.picasso.adesk.com/v1/wallpaper/album/${id}/wallpaper
		// 		// 图片评论 http://service.picasso.adesk.com/v2/wallpaper/wallpaper/${id}/comment
		// 		// 接口文档地址：https://www.showdoc.cc/414855720281749?page_id=3680857125411215
		// 	})
		// 	.then(res=>{
		// 		console.log(res);
		// 		this.Recommends = res.res.homepage[1].items;
		// 	})
		// },
		methods: {
			onClickItem(e) {
				if (this.current !== e.currentIndex) {
					this.current = e.currentIndex;
				}
			}
		},
		components: {
			homeAlbum,
			homeNew,
			homeCategory,
			homeRecommend,
			uniSegmentedControl
			
		}
	}
</script>

<style lang="scss" scoped>
	.home_tab{
		.home_tab_title{
			position:relative;
			.title_inner{
				width:60%;
				margin:0 auto;
			}
			.iconsearch{
				width:30rpx;
				height:30rpx;
				background-color: red;
				position:absolute;
				top:50%;
				transform:translateY(-50%);
				right:5%;
			}
		}
	}
</style>
