<template>
	<view>
		video-categroy
	</view>
</template>

<script>
	export default{
		props:{
			objurl:Object
		},
		data(){
			return{
				
			}
		},
		watch:{
			objurl(){
				console.log("dae");
				console.log(this.objurl);
			}
		},
		 mounted() {
		 	console.log("dae1");
		 	console.log(this.objurl);
		 }
	}
</script>

<style>
	
</style>