<template>
	<view class="setting">
		<view class="header">
			<image src="../../static/setting/back.png" mode=""></image>
			<view class="text">
				二维码设置
			</view>
		</view>
		<view class="content">
			
		</view>
	</view>
</template>

<script>
	import drawQrcode from '../../js_sdk/weapp-qrcode.js'
	export default {
		data() {
			return {
				ewm:'',
			}
		},
		onLoad() {

		},
		methods: {
			tel(){
				var that = this
				uni.scanCode({
					success:function(res){
						console.log(res.scanType);
						that.ewm = res.result
					}
				});
			},
			// 点击生成 二维码
			make() {
				new drawQrcode('qrcode', {
					text: this.ewm,
					width: 100,
					height: 100,
					showLoading: true, // 是否显示loading
					loadingText: '二维码生成中', // loading文字
					colorDark: "#333333",
					colorLight: "#FFFFFF",
					correctLevel: drawQrcode.CorrectLevel.H,
					callback:(e)=>{
						console.log(e)
					}
				})
			}
		}
	}
</script>

<style lang="scss" scoped>
	.setting{
		width: 100vw;
		height: 100vh;
		background: url(../../static/setting/bg.png) no-repeat 0 0;
		.header{
			display: flex;
			align-items: center;
			&>image{
				width: 24rpx;
				height: 24rpx;
				justify-self: flex-start;
			}
			.text{
				justify-self: center;
			}
		}
		.content{
			
		}
	}
</style>
