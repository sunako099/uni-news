<template>
	<view class="user">
		<view class="top">
			<image src="../../static/iconfont/his.png" mode=""></image>
			历史记录
			<view class="text"></view>
		</view>
		<view class="content">
			<view class="row" v-for="row in 10">
				<newsbox></newsbox>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				
			};
		}
	}
</script>

<style lang="scss">
	.user{
		.top{
			padding: 50rpx 0;
			background: #f8f8f8;
			color: #555;
			display: flex;
			flex-direction: column;
			justify-content: center;
			align-items: center;
			image{
				width: 150rpx;
				height: 150rpx;
			}
			.text{
				font-size: 38rpx;
				padding-top: 20rpx;
			}
		}
	}
	.content{
		padding: 30rpx;
		.row{
			border-bottom: 1px dotted #efefef;
			padding: 20rpx 0;
		}
	}
</style>
