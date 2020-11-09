<template>
	<view class="content">
		<view class="advertising">
			<image src="../../static/index/index_bg.png" mode=""></image>
		</view>
		<view class="content_bot">
			<view class="qrcode" id='qr'>
				<!-- <image src="../../static/index/index_bg.png" mode=""></image> -->
				<canvas class="qr_img" canvas-id="qrcode" ></canvas>
			</view>
			<view class="scan">
				<image src="../../static/index/scan.png" mode=""></image>
				<view>
					当前为 {{ type }} 收款码
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	// 引入生成二维码的插件
	import drawQrcode from '../../js_sdk/weapp-qrcode.js'
	export default {
		data() {
			return {
				// 广告数据
				advData: [],
				// 二维码数据
				qrCodeData: '',
				// 支付方式
				type: '',
				qrWidth: 0,
				qrHeight: 0,
			}
		},
		onShow() {
			//  获取本地存储的二维码数据/二维码格式
			this.type = uni.getStorageSync('type')
			this.qrCodeData = uni.getStorageSync('ewm')
			console.log("type:", this.type, "qrcode:", this.qrCodeData)
			// 渲染canvas
			
		},
		mounted() {
			//  先获取二维码容器的宽高
			uni.createSelectorQuery().in(this).select('#qr').boundingClientRect().exec((res)=>{
				// console.log(res[0])
				var W = res[0].width
				var calc = 277/287
				// 生成的图片的宽高
				var ws = parseInt( W * calc)
				this.qrWidth = ws
				this.qrHeight = ws
				// console.log(11111, this.qrHeight, this.qrWidth)
				this.make()
			})
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
			make() {
				console.log(this.qrWidth, this.qrHeight)
				new drawQrcode('qrcode', {
					text: this.qrCodeData,
					width: this.qrWidth,
					height: this.qrHeight,
					showLoading: true, // 是否显示loading
					loadingText: '二维码生成中', // loading文字
					colorDark: "#333333",
					colorLight: "#FFFFFF",
					correctLevel: drawQrcode.CorrectLevel.H
				})
			}
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
			left: 0;
			right: 0;
			margin: auto;
			width: calc(100vw - 30px);
			// margin: 0 15rpx;
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
				.qr_img{
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
