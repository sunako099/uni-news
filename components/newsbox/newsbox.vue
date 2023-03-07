<template>
	<view class="newsbox"  @click.native="goDatil(item)">
		<view class="pic">
			<image :src="item.picurl" mode="aspectFill"></image>
		</view>
		<view class="text">
			<view class="title">{{item.title}}</view>
			<view class="info" v-if="!item.looktime">
				<text>{{item.author}}</text>
				<text>{{item.hits}}浏览</text>
			</view>
			<view class="info" v-else>
				<text>浏览时间：
				<uni-dateformat :date="item.looktime"></uni-dateformat></text>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		name:"newsbox",
		props:{
			item:{
				type:Object,
				default(){
					return{
						title:"",
						author:"",
						hits:0,
						picurl:"",
						looktime:""
					}
				}
			}
		},
		data() {
			return {
				
			};
		},
		methods:{
			goDatil(item){
				uni.navigateTo({
					url:`/pages/dtail/dtail?cid=${item.classid}&id=${item.id}`
				})
			}
		}
	}
</script>

<style lang="scss">
	.newsbox{
		display: flex;
		.pic{
			width: 230rpx;
			height: 160rpx;
			image{
				width: 100%;
				height: 100%;
			}
		}
		.text{
			flex: 1;
			padding-left: 20rpx;
			display: flex;
			flex-direction: column;
			justify-content: space-between;
			.title{
				font-size: 38rpx;
				color: #333;
				display: -webkit-box;
				    text-overflow: ellipsis;
				    overflow: hidden;
				    -webkit-box-orient: vertical;
				    -webkit-line-clamp: 2;//当属性值为3，表示超出3行隐藏
			}
			.info{
				font-size: 26rpx;
				color: #999;
				text{
					padding-right: 30rpx;
				}
			}
		}
	}
</style>