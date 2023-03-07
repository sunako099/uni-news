<template>
	<view class="home">
			<scroll-view scroll-x class="navScroll" >
				<view class="item" :class="index==navIndex?'active':''" 
				v-for="(item,index) in 10" @click="clickNav(index)">国内</view>
			</scroll-view>
		<view class="content">
			<view class="row"  v-for="row in 10">
				<newsbox></newsbox>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				navIndex:0
			}
		},
		onLoad() {

		},
		methods: {
			clickNav(e){
				this.navIndex=e;
			}
		}
	}
</script>

<style lang="scss" scoped>
	.navScroll{
		height: 100rpx;
		background: #f7f8fa;
		white-space: nowrap;
		position: fixed;
		top: var(--window-top);
		left: 0;
		z-index: 10;
		.item{
			font-style: 40rpx;
			display: inline-block;
			line-height: 100rpx;
			padding: 0 30rpx;
			color: #333;
			&.active{
				color: #31c27c;
			}
		}
		/deep/::-webkit-scrollbar{
			width: 4px !important;
			height: 1px !important;
			overflow: auto !important;
			background: transparent !important;
			-webkit-appearance: auto !important;
			display: block;
		}
	}
	.content{
		padding: 30rpx;
		padding-top: 130rpx;
		.row{
			border-bottom: 1px dotted #efefef;
			padding: 20rpx 0;
		}
	}
</style>
