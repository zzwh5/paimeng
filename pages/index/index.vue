<template>
	<view class="content">
		<view class="swiper">
			<u-swiper :list="list" effect3d></u-swiper>
		</view>
		<view class="ewm">
			
		</view>
		<view class="button">
			<u-button type="primary" size = "mini">点击设置</u-button>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				list: [
					{
						image: 'https://cdn.uviewui.com/uview/swiper/1.jpg',
						title: '昨夜星辰昨夜风，画楼西畔桂堂东'
					},
					{
						image: 'https://cdn.uviewui.com/uview/swiper/2.jpg',
						title: '身无彩凤双飞翼，心有灵犀一点通'
					},
					{
						image: 'https://cdn.uviewui.com/uview/swiper/3.jpg',
						title: '谁念西风独自凉，萧萧黄叶闭疏窗，沉思往事立残阳'
					}
				],
			}
		},
		onLoad() {

		},
		methods: {
			tel(){
				uni.scanCode({
					success:function(res){
						console.log(JSON.stringify(res.result));
					}
				});
			}
		}
	}
</script>

<style lang="scss" scoped>
	.content{
		.ewm{
			width: 100%;
			height: 750rpx;
			margin-top: 20rpx;
			background: #00c6ff;  /* fallback for old browsers */
			background: -webkit-linear-gradient(to right, #0072ff, #00c6ff);  /* Chrome 10-25, Safari 5.1-6 */
			background: linear-gradient(to right, #0072ff, #00c6ff); /* W3C, IE 10+/ Edge, Firefox 16+, Chrome 26+, Opera 12+, Safari 7+ */
			border-radius: 20rpx;
		}
		.button{
			margin-top: 20rpx;
		}
	}
</style>
