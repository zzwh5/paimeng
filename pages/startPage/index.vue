<template>
	<view class="content">
		<!-- 跳过模块 -->
		<view class="skip" @click="jumpTo(0)">
			跳过<span>{{ skipTime }}</span>s
		</view>
		<view class="pic">
			<image src="@/static/startPage/startPic.png" mode=""></image>
		</view>
		<view class="pay">
			<view class="pay_title">派盟支付</view>
			<view class="pay_msg">
				<view>
					<text style="color: #FF4932;">扫码</text>支付
				</view>
				<view>
					<text style="color: #FF4932;">一键</text>设置
				</view>
				<view>
					<text style="color: #FF4932;">快捷</text>方便
				</view>
			</view>
		</view>
		<view class="btn">
			<view class="btn_left" @click="jumpTo(1)">
				设置二维码
			</view>
			<view class="btn_right" @click="jumpTo(2)">
				展示二维码
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				skipTime: 5,
				timer: null
			};
		},
		created() {
			this.changeTime()
		},
		watch:{
			skipTime(newV, oldV){
				if ( newV === 0) {
					clearInterval(this.timer)
					uni.redirectTo({
						url: '/pages/index/index'
					})
				}
			}
		},
		methods:{
			changeTime() {
				if(this.timer === null){
					console.log(1111)
					this.timer = setInterval(() => {
						this.skipTime--
					}, 1000)
				}
			},
			jumpTo(i) {
				if (this.timer) {
					clearInterval(this.timer)
				}
				clearInterval(this.timer)
				if (i == 1) {
					uni.redirectTo({
						url: '/pages/setting/settingng'
					})
					return
				}else if (i == 2) {
					uni.redirectTo({
						url: '/pages/index/index'
					})
					return
				} else if (i == 0) {
					uni.redirectTo({
						url: '/pages/index/index'
					})
				}
 			}
		}
	}
</script>

<style lang="scss">
	.content{
		height: 100vh;
		width: 100vw;
		display: flex;
		flex-direction: column;
		justify-content: space-around;
		align-items: center;
		// background-color: red;
		position: relative;
		.skip{
			position: absolute;
			right: 40rpx;
			top: 40rpx;
			width: 80rpx;
			height: 50rpx;
			font-size: 22rpx;
			line-height: 50rpx;
			text-align: center;
			background-color: rgba(204,204,204, .5);
		}
		.pic{
			width: 560rpx;
			height: 658rpx;
			image{
				width: 100%;
				height: 100%;;
			}
		}
		.pay{
			text-align: center;
			font-size: 36rpx;
			font-family: PingFang SC Medium, PingFang SC Medium-Medium;
			font-weight: 500;
			color: #333333;
			.pay_title{
				font-size: 40rpx;
				margin: 20rpx 0;
			}
			.pay_msg{
				width: 490rpx;
				font-size: 34rpx;
				display: flex;
				flex-direction: row;
				justify-content: space-around;
			}
		}
		.btn{
			width: 100%;
			height: 80rpx;
			display: flex;
			flex-direction: row;
			justify-content: space-around;
			&>view{
				width: 280rpx;
				height: 80rpx;
				border-radius: 40rpx;
				font-size: 34rpx;
				font-family: Source Han Sans CN Regular, Source Han Sans CN Regular-Regular;
				font-weight: bold;
				text-align: justifyLeft;
				color: #ffffff;
				line-height: 80rpx;
			}
			.btn_left{
				background-color: #FF9F49;
				text-align: center;
			}
			.btn_right{
				text-align: center;
				background-color: #454DFB;
			}
		}
	}
</style>
