<template>
	<view class="detail">
		<view class="title">{{detail.title}}</view>
		<view class="info">
			<view class="author">{{detail.author}}</view>
			<view class="time">
				<uni-dateformat :date="detail.posttime*1000"></uni-dateformat>
			</view>
		</view>
		<view class="content">
			<rich-text :nodes="detail.content"></rich-text>
		</view>
		<view class="description">
			描述
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				options: null,
				detail: {}
			};
		},
		onLoad(e) {
			this.options = e;
			this.getDetail()
		},
		methods: {
			getDetail() {
				uni.request({
					url: "https://ku.qingnian8.com/dataApi/news/detail.php",
					data: this.options,
					success: (res) => {
						res.data.content = res.data.content.replace(/<img/gi, '<img style="max-width:100%"')
						this.detail = res.data
						this.saveHistory()
						uni.setNavigationBarTitle({
							title: this.detail.title
						})
					}
				})
			},
			saveHistory() {
				let historyArr = uni.getStorageSync("historyArr") || [];
				let item = {
					id: this.detail.id,
					classid: this.detail.classid,
					picurl: this.detail.picurl,
					title: this.detail.title,
					looktime: Date.now()
				}
				let index = historyArr.findIndex(i => {
					return i.id == this.detail.id
				})
				
				if(index>=0){
					historyArr.splice(index,1)
				}
				historyArr.unshift(item)
				historyArr=historyArr.slice(0,10)
				uni.setStorageSync("historyArr", historyArr)
			}
		}
	}
</script>

<style lang="scss">
	.detail {
		padding: 30rpx;

		.title {
			font-size: 46rpx;
			color: #333;
		}

		.info {
			background: #f6f6f6;
			padding: 20rpx 20rpx;
			font-size: 25rpx;
			color: #666;
			display: flex;
			justify-content: space-between;
			margin: 40rpx 0;
		}

		.content {
			padding-bottom: 50rpx;

			/deep/ img {
				max-width: 100%;
			}
		}

		.description {
			background: #fef0f0;
			font-size: 26rpx;
			padding: 20rpx;
			color: #f89898;
			line-height: 1.8em;
		}
	}
</style>
