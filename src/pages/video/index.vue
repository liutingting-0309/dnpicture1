<template>
	<view>
		<view class="video_tab_title">
			<view class="title_inner">
				<uni-segmented-control :current="current" :values="items.map(v=>v.title)" @clickItem="onClickItem" style-type="text" active-color="#d98cb8">
				</uni-segmented-control>
			</view>
			<view class="iconfont iconsearch">
				<!-- <img src="./static/icon/ordermanagement.png" alt="" style="width:30rpx;height:30rpx"> -->
			</view>
		</view>	
		<view class="video-body">
			<video-recommend v-if="current < 4"></video-recommend>
			<video-categroy v-else></video-categroy>
		</view>
		
	</view>
</template>

<script>
	import videoCategroy from "./video-categroy";
	import videoRecommend from "./video-recommend";
	import {uniSegmentedControl} from "@dcloudio/uni-ui";
	export default {
		data() {
			return {
				params:{
					limit:"30",
					skip:0,
					order:"hot"
				},
				items: [
					{title:'推荐'},
					{title:'娱乐'},
					{title:'最新'},
					{title:'热门'},
					{title:'分类'}
					],
				current: 0
			}
		},
		onLoad() {
			this.getlist();
		},
		methods: {
			getlist(){
				this.request({
					url:"http://service.picasso.adesk.com/videoimg/v1/videowp/featured",
					data:this.params
				})
				.then(res =>{
					console.log(res)
				})
			},
			onClickItem(e) {
				if (this.current !== e.currentIndex) {
					this.current = e.currentIndex;
				}
			}
		},
		components:{
			videoCategroy,
			videoRecommend
		}
	}
</script>

<style lang="scss" scoped>
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
</style>
