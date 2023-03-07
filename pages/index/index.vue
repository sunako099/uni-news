<template>
	<view class="home">
		<scroll-view scroll-x class="navScroll">
			<view class="item" :class="index==navIndex?'active':''" v-for="(item,index) in navList" :key="item.id"
				@click="clickNav(index,item.id)">{{item.classname}}</view>
		</scroll-view>
		<view class="content">
			<view class="row" v-for="item in newsArr" :key="item.id">
				<newsbox :item="item"></newsbox>
			</view>
		</view>

		<view class="loading" v-if="newsArr.length">
			<view v-show="loading==1">数据加载中...</view>
			<view v-show="loading==2">没有更多了</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				navIndex: 0,
				navList: [],
				newsArr: [],
				currentPage: 1,
				loading: 0 //0：默认 1：加载中 2：没有了
			}
		},
		onLoad() {
			this.getNavData();
			this.getNewsData()
		},
		onReachBottom() {
			if (this.loading == 2) {
				return
			}
			this.loading = 1;
			this.currentPage++;
			
			this.getNewsData(this.navIndex)
		},
		methods: {
			clickNav(e, id) {
				this.navIndex = e;
				this.currentPage = 1;
				this.newsArr = [];
				this.loading = 0;
				this.getNewsData(id)
			},
			getNavData() {
				uni.request({
					url: "https://ku.qingnian8.com/dataApi/news/navlist.php",
					success: (res) => {
						this.navList = res.data
					}
				})
			},
			getNewsData(id) {
				uni.request({
					url: "https://ku.qingnian8.com/dataApi/news/newslist.php",
					data: {
						cid: id,
						page: this.currentPage
					},
					success: (res) => {
						if (res.data.length == 0) {
							this.loading = 2
						}
						this.newsArr = [...this.newsArr, ...res.data]
					}
				})
			}
		}
	}
</script>

<style lang="scss" scoped>
	.navScroll {
		height: 100rpx;
		background: #f7f8fa;
		white-space: nowrap;
		position: fixed;
		top: var(--window-top);
		left: 0;
		z-index: 10;

		.item {
			font-style: 40rpx;
			display: inline-block;
			line-height: 100rpx;
			padding: 0 30rpx;
			color: #333;

			&.active {
				color: #31c27c;
			}
		}

		/deep/::-webkit-scrollbar {
			width: 4px !important;
			height: 1px !important;
			overflow: auto !important;
			background: transparent !important;
			-webkit-appearance: auto !important;
			display: block;
		}
	}

	.content {
		padding: 30rpx;
		padding-top: 130rpx;

		.row {
			border-bottom: 1px dotted #efefef;
			padding: 20rpx 0;
		}
	}

	.loading {
		text-align: center;
		font-size: 26rpx;
		color: #888;
		line-height: 2em;
	}
</style>
