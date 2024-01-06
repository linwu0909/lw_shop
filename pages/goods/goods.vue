<template>
	<view class="goods_list">
		<goods-list :goods="goods" @goodsItemClick="goDetail"></goods-list>
		<view class="isOver" v-if="flag">-----我是有底线的-----</view>
	</view>
</template>

<script>
	import GoodsList from '@/components/goods-list/goods-list.vue'
	export default {
		components: {GoodsList},
		data() {
			return {
				pageIndex: 1,
				goods: [],
				flag: false
			}
		},
		onLoad() {
			this.getGoodsList()
		},
		onReachBottom() {
			if (this.goods.length < this.pageIndex*10) {
				return this.flag = true
			}
			this.pageIndex++
			this.getGoodsList()
		},
		async onPullDownRefresh() {
			this.pageIndex = 1;
			this.goods = []
			this.flag = false;
			await this.getGoodsList()
			uni.stopPullDownRefresh()
		},
		methods: {
			async getGoodsList() {
				const res = await this.$myRequest({
					url: '/api/getgoods?pageindex=' + this.pageIndex
				})
				this.goods = [...this.goods, ...res.data.message]
			},
			goDetail(id) {
				uni.navigateTo({
					url: '/pages/goods-detail/goods-detail?id='+id
				})
			}
		}
	}
</script>

<style lang="scss">
	.goods_list {
		background: #eee;
	}
	.isOver{
		width: 100%;
		height: 50px;
		line-height: 50px;
		text-align: center;
		font-size: 28rpx;
	}
</style>
