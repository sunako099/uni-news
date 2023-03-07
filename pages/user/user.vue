<template>
	<view class="user">
		<view class="top">
			<image src="../../static/iconfont/his.png" mode=""></image>
			历史记录
			<view class="text"></view>
		</view>
		<view class="content">
			<view class="row" v-for="item in listArr">
				<newsbox :item="item"></newsbox>
			</view>
		</view>
		<view class="nohistory" v-if="!listArr.length">
			<image src="../../static/01c8f15aeac135a801207fa16836ae.jpg@1280w_1l_2o_100sh.jpg" mode="widthFix"></image>
			<view class="text">暂无浏览记录</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				listArr: []
			};
		},
		onLoad() {
			this.getData()
		},
		methods: {
			getData() {
				let historyArr = uni.getStorageSync("historyArr") || []
				this.listArr = historyArr;
			}
		}
	}
</script>

<style lang="scss">
	.user {
		.top {
			padding: 50rpx 0;
			background: #f8f8f8;
			color: #555;
			display: flex;
			flex-direction: column;
			justify-content: center;
			align-items: center;

			image {
				width: 150rpx;
				height: 150rpx;
			}

			.text {
				font-size: 38rpx;
				padding-top: 20rpx;
			}
		}
	}

	.content {
		padding: 30rpx;

		.row {
			border-bottom: 1px dotted #efefef;
			padding: 20rpx 0;
		}
	}
	.nohistory{
			display: flex;
			flex-direction: column;
			justify-content: center;
			align-items: center;
			image{
				width: 450rpx;
			}
			.text{
				font-size: 26rpx;
				color:#888;
			}
		}
</style>
