<script>
export default {
	onLaunch: function() {
		console.log('App Launch');
		uni.getStorage({
			key: 'token',
			success: function(res) {
				console.log(res.data);
				if (res.data == 'ok') {
					uni.switchTab({
						url: '/pages/home/home',
						fail(err) {
							console.log(err);
						}
					});
				}
			}
		});
	},
	onShow: function() {
		console.log('App Show');
	},
	onHide: function() {
		console.log('App Hide');
	}
};
</script>

<style>
/*每个页面公共css */
</style>
