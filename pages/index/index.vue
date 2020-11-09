<template>
	<view class="content">
		<view class="advertising">
			<image src="../../static/index/index_bg.png" mode=""></image>
		</view>
		<view class="content_bot">
			<view class="qrcode">
				<image src="../../static/index/index_bg.png" mode=""></image>
			</view>
			<view class="scan">
				<image src="../../static/index/scan.png" mode=""></image>
				<view>
					当前为{{ payMethod }}收款码
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				// 广告数据
				advData: [],
				payMethod: '支付宝'
			}
		},
		onLoad() {

		},
		methods: {
			//  请求广告数据
			// getAdvData(){
			// 	var that = this
			// 	uni.request({
			// 		url: '',
			// 		data: 
			// 	})
			// }
		}
	}
</script>

<style lang="scss" scoped>
	.content{
		height: 100vh;
		width: 100vw;
		position: relative;
		box-sizing: border-box;
		overflow: hidden;
		.advertising{
			position: absolute;
			left: 0;
			top: 0;
			width: 100%;
			height: 100%;
			&>image{
				display: block;
				height: 100%;
				width: 100%;
			}
		}
		.content_bot{
			position: absolute;
			bottom: 16rpx;
			width: calc(100vw - 30px);
			margin: 0 15rpx;
			padding: 15rpx;
			box-sizing: border-box;
			border-radius: 10rpx;
			background: rgba(0,0,0, .3);
			overflow: hidden;
			display: flex;
			flex-direction: row;
			.qrcode{
				width: 287rpx;
				height: 287rpx;
				padding: 10rpx;
				box-sizing: border-box;
				background-color: #fff;
				&>image{
					display: block;
					width: 100%;
					height: 100%;
				}
			}
			.scan{
				flex: 1;
				display: flex;
				flex-direction: column;
				justify-content: space-around;
				align-items: center;
				&>image{
					display: block;
					width: 207rpx;
					height: 106rpx;
				}
				&>view{
					font-size: 30rpx;
					color: #FFFFFF;
					font-family: PingFang SC Medium, PingFang SC Medium-Medium;
					font-weight: bold;
				}
			}
		}
	}
</style>
