<template>
	<view class="news_detail">
		<text class="title">{{detail.title}}</text>
		<view class="info">
			<text>发表时间：{{detail.add_time}}</text>
			<text>浏览：{{detail.click}}</text>
		</view>
		<view class="content">
			<rich-text :nodes="detail.content"></rich-text>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				id: 0,
				detail: {}
			}
		},
		onLoad(options) {
			this.id = options.id;
			this.getNewsDetail();
		} ,
		methods: {
			async getNewsDetail(){
				const res = await this.$myRequest({
					url: '/api/getnew/'+this.id
				})
				this.detail = res.data.message
			}
		}
	}
</script>

<style lang="scss">
.news_detail {
	font-size: 30rpx;
	padding: 0 20rpx;
	.title {
		text-align: center;
		width: 710rpx;
		display: block;
		margin: 20rpx 0;
	}
	.info {
		display: flex;
		justify-content: space-between;
	}
}
</style>
