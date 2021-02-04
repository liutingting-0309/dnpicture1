<template>
	<view>
		<view class="videoplay_box">
			<view class="videoplay_btn">
				<view class="videoplay_btna">1</view>
				<view class="videoplay_btnb">2</view>
			</view>
			<view class="videoplay_body">
				<image class="videoplay_img" src="../../static/icon/commoditymanagement.png"></image>
			</view>
			<view class="videoplay_sbumit">
				立即播放
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				
			}
		},
		methods: {
			
		}
	}
</script>

<style lang='scss' scoped>
	.videoplay_box{
		position: relative;
		padding-top:100rpx;
		.videoplay_btn{
			position: absolute;
			top:20rpx;
			right:10rpx;
			display: flex;
			text-align: center;
			.videoplay_btna{
				width:50rpx;
				height:50rpx;
				background-color: pink;
				border-radius: 50%;
				margin-right:10rpx;
			}
			.videoplay_btnb{
				width:50rpx;
				height:50rpx;
				background-color: blue;
				border-radius: 50%;
			}
		}
		.videoplay_body{
			background-color: red;
			.videoplay_img{
				width:100%;
			}
		}
		.videoplay_sbumit{
			background-color: rgba($color: #000000, $alpha: 0.4);
			width:300rpx;
			height:75rpx;
			line-height: 75rpx;
			border:1rpx solid red;
			border-radius: 40rpx;
			text-align: center;
			margin:30rpx auto 0 ;
		}
	}
</style>
