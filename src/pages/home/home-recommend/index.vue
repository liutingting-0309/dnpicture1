<template>
	<view>
		<!-- <img :src="Recommends" alt=""> -->
		<!-- {{Recommends[1].thumb}} -->
		
	</view>
</template>

<script>
	export default {
		data() {
			return {
				// 推荐列表
				props:{
					Recommends:String
				},
				 recommends:[]
			}
		},
		onLoad(){
			console.log("mounted");
			this.request({
				url: "http://service.picasso.adesk.com/v3/homepage/vertical",
				data: {
					// 要获取几条
					limit: 30,
					// 关键字
					order: "hot",
					// 要跳过几条，
					skip: 0
					}
				})
				.then(res =>{
					console.log(res);
					this.recommends = res.res.homepage[1].items;
				})
		},
		methods: {
			
		}
	}
</script>

<style>

</style>
