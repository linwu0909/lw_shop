<template>
	<view class="contact">
		<image class="img" src="http://www.itcast.cn/2018czydz/images/gywmban.jpg"></image>
		<view class="info">
			<view @click="callPhone">联系电话：400-618-9090（ 点击拨打 ）</view>
			<view>地址：浙江省杭州市西湖区西湖公园111号</view>
		</view>
		<map class="map" :longitude="longitude" :latitude="latitude" :markers="markers" :scale="scale"></map>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				longitude: '120.12792',
				latitude: '30.228932',
				scale: 13,
				markers: [
					{
						longitude: '120.12792',
						latitude: '30.228932',
						iconPath: '../../static/logo.png',
						width: 30,
						height: 30
					}
				]
			}
		},
		methods: {
			callPhone()  {
				uni.makePhoneCall({
					phoneNumber: '400-618-9090'
				})
			}
		}
	}
</script>

<style lang="scss">
.contact {
	.img {
		width: 750rpx;
		height: 320rpx;
	}
	.info {
		padding: 10rpx 20rpx;
		font-size: 30rpx;
		view {
			line-height: 80rpx;
			border-bottom: 1px solid #eee;
		}
	}
	.map {
		width: 750rpx;
		height: 750rpx;
	}
}
</style>
