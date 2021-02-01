<template>
	<!-- 加v-if是为了防止数据未加载出来时 显示undefined -->
	<scroll-view @click="handleToLower()" class="recommend_view" scroll-y v-if="recommends.length>0">
		<!-- 推荐 开始 -->
		<view class="recommend_wrap">
			<navigator class="recommend_item" v-for="item in recommends" :key="item.id" :url="`/pages/album/index?id=${item.target}`">
				<image class="recommend_img" mode="widthFix" :src="item.thumb"></image>
			</navigator>
		</view>
		<!-- 推荐 结束 -->
		<!-- 月份 开始 -->
		<view class="moneths_wrap">
			<view class="moneths_title">
				<view class="moneths_title_info">
					<view class="moneths_info">
						<text class="info_day">{{montheslist.DD}} /</text>
					   {{montheslist.MM}}月
					</view>
					<view class="moneths_text">{{montheslist.title}}</view>
				</view>
				<view class="moneths_title_more">更多 ></view>
			</view>
			<view  class="moneths_content" >
				<view class="moneths_imgs" v-for="(item,index) in montheslist.items" :key="item.id">
				<go-detail :list="montheslist.items" :index="index">
					<image class="moneths_img" :src="item.thumb+item.rule.replace('$<Height>', 360)" mode="aspectFill"></image>
				</go-detail>
				</view>
			</view>
		</view>
		<!-- 月份 结束 -->
		<!-- 热门 开始 -->
		<view class="hot_wrap">
			<view class="hot_title"><text>热门</text></view>
			<view class="hot_imgs">
				<view class="hot_img" v-for="item in hotlist" :key="item.id">
						<image class="hot_image" :src="item.thumb" mode="widthFix"></image>				
				</view>
			</view>
		</view>
		<!-- 热门 结束 -->
	</scroll-view>
</template>

<script>
	import moment from "moment";
	import goDetail from "@/components/goDetail";
	export default {
		data() {
			return {
				// 推荐列表
				// props:{
				// 	Recommends:String
				// },
				recommends: [],
				// 月份列表
				montheslist:[],
				// 热门列表
				hotlist:[],
				params: {
					// 要获取几条
					limit: 30,
					// 关键字
					order: "hot",
					// 要跳过几条，
					skip: 0
				},
				hasMore:true,
			}
		},
		mounted() {
			this.getList();
		},
		components:{
			goDetail
		},
		methods: {
			// 请求数据
			getList(){
				this.request({
						url: "http://service.picasso.adesk.com/v3/homepage/vertical",
						data: this.params
					})
					.then(res => {
						if(res.res.vertical.length === 0){
							this.hasMore = false;
							return
						}
						if(this.recommends.length === 0){
						// 推荐模块
						this.recommends = res.res.homepage[1].items;
						// 月份模块
						this.montheslist = res.res.homepage[2];
						// 将时间戳  改成 18号/月 moment.js
						this.montheslist.MM = moment(this.montheslist.stime).format("MM");
						this.montheslist.DD = moment(this.montheslist.stime).format("DD");
						}
						// 热门模块
						// 数组拼接模式
						this.hotlist = [...this.hotlist,...res.res.vertical];
						// this.hotlist = res.res.vertical;
						// console.log(this.hotlist);
						
					});
			},
			// 滚动条触底事件
			handleToLower(){
				// 1.修改参数 skip+=limit;
				// 重新发送请求getList()
				// 3.请求回来成功 hots 数据叠加
				if(this.hasMore){
					this.params.skip += this.params.limit;
					this.getList();
				}else{
					// 弹窗提示用户
					uni.showToast({
						title:"没有数据了",
						icon:"none"
					})
				}
			}
		}
	}
</script>

<style lang="scss" scoped>
	.recommend_view{
		// height：屏幕的高度 - 头部标题的高度
		height: calc( 100vh - 36px );
	}
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
			box-shadow:2px 2px 2px #eee;
			display: flex;
			flex-wrap: wrap;
			justify-content: space-between ;	
			.moneths_title_info{
				display: flex;
				.moneths_info{
					margin-left:10rpx;
					color:#ff557f;
					font-size: 30rpx;
					.info_day{
						font-size:45rpx;
					}
				}
				.moneths_text{
					font-size:30rpx;
					margin-left: 10rpx;
					text-align: center;
					// border:1rpx solid red;
					line-height: 60rpx;
				}
			}
			.moneths_title_more{
				margin-right:15rpx;	
				line-height: 60rpx;
				font-size:30rpx;
				font-weight: 700;
				color:#ff557f;
			}
		}	
		.moneths_content{
			display:flex;
			flex-wrap:wrap;
			width:100%;
				.moneths_imgs{
					width:33%;
					margin-left:2rpx;
					.moneths_img{
						width:100%;
						display: block;
					}
				}		
		}
	}
	.hot_wrap{
		.hot_title{
			margin: 5rpx 10rpx;
			padding-left:5rpx;
			border-left:10rpx solid #ff557f;
			font-size: 30rpx;
			font-weight: 700;
		}
		.hot_imgs{
			display:flex;
			flex-wrap: wrap;
			width:100%;
			margin-left:4rpx;
			.hot_img{
				width:33%;
				.hot_image{
					width:100%;
					display:block;
					vertical-align:center;
				}
			}
		}
	}
	
			
</style>
