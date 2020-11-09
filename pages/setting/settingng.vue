<template>
	<view class="setting" :style="{'background':'url('+bg+')'}">
		<view class="header">
			<!-- <view class="img">
				<image src="../../static/setting/back.png" mode=""></image>
			</view> -->
			二维码设置
		</view>
		<view class="content">
			<!-- 选择微信或者支付宝 -->
			<view class="change">
				<view class="title" :style="{'background-color':bgChange}">
					选择二维码终端
				</view>
				<view class="wx-zfb">
					<view class="zfb" @click="changeMethod(0)">
						<image src="../../static/setting/zfb.png" mode=""></image>
						<text>支付宝</text>
					</view>
					<view class="wx" @click="changeMethod(1)">
						<image src="../../static/setting/wx.png" mode=""></image>
						<text>微信</text>
					</view>
				</view>
			</view>
			<!-- 中间区域的图片 -->
			<view class="money">
				<image :src="money" mode=""></image>
			</view>
			<view class="ewm" :style="{'background':bgEwm}">
				<view class="img imgs" id="img">
					<canvas canvas-id="qrcode" :style="{'width':'250rpx','height':'250rpx'}"></canvas>
				</view>
				<view class="text">
					您的{{type==0?'支付宝':'微信'}}二维码
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	import drawQrcode from '../../js_sdk/weapp-qrcode.js'
	export default {
		data() {
			return {
				// 当前二维码的类型 0 支付宝 1 微信
				type:0,
				// 画布的宽高
				canvasW:0
			}
		},
		computed:{
			// 页面的背景图
			bg(){
				if(this.type === 0){
					return require('../../static/setting/bg.png')
				}else{
					return require('../../static/setting/bg1.png')
				}
			},
			// money的图片
			money(){
				if(this.type === 0){
					return require('../../static/setting/money.png')
				}else{
					return require('../../static/setting/money1.png')
				}
			},
			// 选择二维码终端的背景图
			bgChange(){
				if(this.type === 0){
					return '#007CFF'
				}else{
					return '#088205'
				}
			},
			// 二维码背景图
			bgEwm(){
				if(this.type === 0){
					return 'rgba(0,124,255,.4)'
				}else{
					return 'rgba(31,153,6,.4)'
				}
			}
		},
		onLoad() {},
		mounted() {
			var that = this
			// dom树生成之后 获取 id="img"的宽高 根据比例得到canvas的宽高
			uni.createSelectorQuery().in(this).select('#img').boundingClientRect().exec((res)=>{
				// console.log(res[0])
				var W = res[0].width
				var calc = 250/287
				// 生成的图片的宽高
				var ws = W * calc
				this.canvasW = ws
			})
		},
		methods: {
			// 点击切换二维码类型
			changeMethod(type){
				var that = this
				this.type = type
				// console.log(this.canvasW)
				uni.scanCode({
					success:function(res){
						var turn = false
						console.log(that.type,res.result)
						if((that.type == 1 && res.result.indexOf('wx')!=-1 ) ||
							(that.type == 0 && res.result.indexOf('ali')!=-1)){
							turn = true
						}else{
							turn = false
						}
						var text = that.type==0?'支付宝':'微信'
						if(!turn){
							uni.showModal({
							    title: '提示',
							    content: '你当前选择的是' + text + ',请出示' + text + '二维码',
								showCancel:false,
							    success: function (res) {
							        if (res.confirm) {
							            // console.log('用户点击确定');
							        } else if (res.cancel) {
							            // console.log('用户点击取消');
							        }
							    }
							});
							return false
						}
						that.ewm = res.result
						uni.setStorage({
						    key: 'type',
						    data: text
						});
						uni.setStorage({
						    key: 'ewm',
						    data: res.result
						});
						// 然后调用生成二维码的函数 生成对应的二维码
						that.make()
					}
				});
			},
			// 点击生成 二维码
			make() {
				new drawQrcode('qrcode', {
					text: this.ewm,
					width: this.canvasW,
					height: this.canvasW,
					showLoading: true, // 是否显示loading
					loadingText: '二维码生成中', // loading文字
					colorDark: "#333333",
					colorLight: "#FFFFFF",
					correctLevel: drawQrcode.CorrectLevel.H
				})
				uni.showToast({
					title:'设置成功',
					icon:'success',
					success() {
						setTimeout(()=>{
							uni.redirectTo({
								url: '../index/index'
							});
						},1000)
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
		background-repeat: no-repeat;
		background-position: 0 0;
		box-sizing: border-box;
		padding-top: calc(var(--status-bar-height) + 41rpx) ;
		.header{
			display: flex;
			align-items: center;
			justify-content: center;
			width: 100%;
			position: relative;
			color: #FFFFFF;
			.img{
				position: absolute;
				left: 25rpx;
				top: 50%;
				transform:translateY(-50%);
				// flex:1;
				&>image{
					width: 24rpx;
					height: 24rpx;
				}
			}
		}
		.content{
			margin-top: 52rpx;
			.change{
				.title{
					width: 279rpx;
					height: 70rpx;
					display: flex;
					align-items: center;
					justify-content: center;
					color: #FFFFFF;
					border-radius: 35rpx 35rpx 0px 0px;
					margin: 0 auto;
				}
				.wx-zfb{
					width: 690rpx;
					height: 186rpx;
					background-color: #FFFFFF;
					margin: 0 auto;
					display: flex;
					align-items: center;
					justify-content: space-between;
					box-sizing: border-box;
					padding-top: 23rpx;
					padding: 23rpx 125rpx 20rpx 132rpx;
					&>view{
						display: flex;
						flex-direction: column;
						justify-content: center;
						&>image{
							width: 96rpx;
							height: 96rpx;
						}
						&>text{
							font-size: 30rpx;
							text-align: center;
							margin-top: 19rpx;
						}
					}
				}
			}
			.money{
				margin-top: 34rpx;
				width: 750rpx;
				height: 358rpx;
				&>image{
					width: 100%;
					height: 100%;
				}
			}
			.ewm{
				width: 690rpx;
				height: 435rpx;
				margin: 0 auto;
				margin-top: 17rpx;
				display: flex;
				flex-direction: column;
				align-items: center;
				justify-content: space-between;
				padding: 39rpx 0 25rpx 0;
				box-sizing: border-box;
				.img{
					width: 287rpx;
					height: 287rpx;
					background: #ffffff;
					display: flex;
					align-items: center;
					justify-content: center;
				}
				.text{
					font-size: 28rpx;
					color: #FFFFFF;
				}
			}
		}
	}
</style>
