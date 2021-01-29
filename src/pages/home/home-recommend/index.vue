<template>
	<view>
		<!-- 推荐 开始 -->
		<view class="recommend_wrap">
			<view class="recommend_item" v-for="item in recommends" :key="item.id">
				<image class="recommend_img" mode="widthFix" :src="item.thumb"></image>
			</view>
		</view>
		<!-- 推荐 结束 -->
		<!-- 月份 开始 -->
		<view class="moneths_wrap">
			<view class="moneths_title">
				<view class="moneths_title_info">
					<view class="moneths_info">
						<text>18 /</text>
					   01月
					</view>
					<view class="moneths_text">你负责美丽</view>
				</view>
				<view class="moneths_title_more">更多 ></view>
			</view>
			<view class="moneths_content"></view>
		</view>
		<!-- 月份 结束 -->
	</view>
</template>

<script>
	export default {
		data() {
			return {
				// 推荐列表
				// props:{
				// 	Recommends:String
				// },
				recommends: []
			}
		},
		mounted() {
			// var that = this;
			// console.log("mounted");
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
				.then(res => {
					console.log(res);
					this.recommends = res.res.homepage[1].items;
				})
		},

		methods: {

		}
	}
</script>

<style lang="scss" scoped>
	.recommend_wrap {
		// flex布局
		display: flex;
		flex-wrap: wrap;
		width:100%;
		.recommend_item {
			width: 49%;
			border: 3rpx solid #fff;
			margin-left:3rpx;
			.recommend_img{
				width:100%;
			// 消除底部空白,默认基线对齐导致	
				display:block;
				vertical-align:center;
			}
		}
	}
	.moneths_wrap{
		.moneths_title{
			display: flex;
			flex-wrap: wrap;
			justify-content: space-between ;	
			.moneths_title_info{
				display: flex;
				.moneths_info{
					color:#ff557f;
				}
				.moneths_text{
					
				}
				.moneths_title_more{
						
					}
			}
		.moneths_content{
					
		}
	}
					
	}
			
</style>
