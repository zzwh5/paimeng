<template>
	<view class="setting">
		<u-button type="primary" size = "mini" @tap="tel">点击录入</u-button>
	</view>
</template>

<script>
	export default {
		data() {
			return {}
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
	
</style>
