<template>
	<view>
		<uni-segmented-control :current="current" :values="items.map(v=>v.title)" @clickItem="onClickItem" style-type="text" active-color="#d98cb8">
		</uni-segmented-control>
		<view class="content">
			<view v-if="current === 0">
				<homeAlbum></homeAlbum>
			</view>
			<view v-if="current === 1">
				<homeCategory></homeCategory>
			</view> 
			<view v-if="current === 2">
				<homeNew></homeNew>
			</view>
			<view v-if="current === 3">
				<homeRecommend></homeRecommend>
			</view>
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
				current: 0
			}
		},
		// onLoad() {
		// 	this.request({
		// 		// 接口不能用
		// 		// url:"http://157.122.54.189:9088/image/v3/homepage/vertical",
		// 		// http://www/showdoc.cc/414855720281749?page_id=367862101729602
		// 		// 豆瓣接口
		// 		url:"https://douban.uieee.com"
		// 	})
		// 	.then(res=>{
		// 		console.log(res);
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

<style>

</style>
