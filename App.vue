<script>
	export default {
		onLaunch: function() {
			console.log('App Launch')
		},
		onShow: function() {
			console.log('App Show')
			// #ifdef APP-PLUS
			plus.navigator.setFullscreen(true) //隐藏状态栏
			plus.navigator.hideSystemNavigation() //隐藏虚拟按键
			// #endif
		},
		onHide: function() {
			console.log('App Hide')
		}
	}
</script>

<style>
	/*每个页面公共css */
</style>
