<template>
	<scroll-view scroll-y>
			<view class="videowp">
				<navigator :url="`/pages/videoplay/videoplay?id=${item.id}`" class="videowp_imgs"  v-for="item in videowp" :key="item.id">
					<image class="videowp_img" :src="item.cover" mode="aspectFill"></image>
			</navigator>
			</view>
	</scroll-view>
</template>

<script>
	export default{
		props:{
			objurl:Object
		},
		data(){
			return{
				videowp:[]
			}
		},
		watch:{
			objurl(){
				console.log("参数发生变化了");
				// console.log(this.objurl);
				this.getlist();
			}
			
		},
		mounted() {
			// console.log("eee1");
			// console.log(this.objurl);
			this.getlist();
		},
		methods:{
			getlist(){
				this.request({
					url:this.objurl.url,
					data:this.objurl.params
				}).then(res=>{
					console.log(res)
					// this.videowp=res.res.viedowp;
					this.videowp = res.res.album;
					console.log(this.videowp);
				})
			},
		}
	}
</script>

<style lang="scss" scoped>
	.videowp{
		display: flex;
		flex-wrap: wrap;
		.videowp_imgs{
			width:33%;
			margin:0 0 3rpx 3rpx;
			.videowp_img{
				width:100%;
				display: block;
			}
		}
	}
</style>