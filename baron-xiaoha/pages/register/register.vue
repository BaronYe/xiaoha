<template>
	<view class="content">
		
		<!-- 图标 -->
		<view class="logo">
			<image src="../../static/images/index/logo.png" class="logo-image"></image>
		</view>
		<!-- 登陆 -->
		<view class="main">
			<view class="title"></view>
			<view class="inputs">
				<view class="inputs-div">
					<input class="input" type="text" placeholder="请输入用户名" placeholder-style="color:#aaa;font-weight:400;" @blur="isname"
					 v-model="name" />
					<view class="employ" v-show="employ">已占用</view>
					<image src="../../static/images/register/right.png" class="ok" v-show="isuser"></image>
				</view>

				<view class="inputs-div">
					<input class="input" :type="type" placeholder="请设置密码" placeholder-style="color:#aaa;font-weight:400;" @blur="check()"
					 v-model="password" />
					<view class="employ" v-show="employ">已占用</view>
					<image :src="showurl" class="show" @click="showon()"></image>
				</view>
				<view class="inputs-div">
					<input class="input" :type="type" placeholder="请确认密码" placeholder-style="color:#aaa;font-weight:400;" @blur="checknumber()"
					 v-model="check_password" />
					<view class="employ" v-show="employ">已占用</view>
					<text class="checknumber" v-show="checkshow">请输入6-20位字母数字组合且保证两次密码一致</text>

					<image :src="showurl" class="show" @click="showon()"></image>
				</view>
			</view>
		</view>
		<!-- 登陆按钮 -->
		<view class="submit" @click="submit">注册</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {

				type: "password",
				isuser: 0, //用户名是否占用
				isemail: 0, //邮箱是否占位
				show: false, // 是否显示密码
				invalid: false, // 邮箱是否符合
				employ: false, //是否被占用
				showurl: '../../static/images/register/showin.png',
				email: '',
				name: '',
				password: '',
				check_password: '',
				checkshow: false
			};
		},
		methods: {
			//密码是否显隐
			showon: function() {
				if (this.show) {
					this.type = 'password';
					this.show = !this.show;
					this.showurl = '../../static/images/register/showin.png';
				} else {
					this.type = 'text';
					this.show = !this.show;
					this.showurl = '../../static/images/register/showon.png';
				}
			},
			isname: function() {
				if (this.name.length > 0) {
					this.isuser = true;
				} else {
					this.isuser = false;
				}
			},
			goLogin: function() {
				uni.navigateBack({
					delta: 1
				});
			},
			checknumber() {
				var reg = /^[A-Za-z0-9]{6,20}$/;
				if (this.password === this.check_password && reg.test(this.password)) {
					this.checkshow = false
				} else {
					this.checkshow = true
				}
			},
			check() {

				if (this.check_password.length > 0) {
					var reg = /^[A-Za-z0-9]{6,20}$/;

					if (this.password === this.check_password && reg.test(this.password)) {
						this.checkshow = false;



					} else {
						this.checkshow = true

					}


				}
			},
			submit() {

				if (this.checkshow === false && this.check_password.length > 0) {

					uniCloud.callFunction({
						name: 'register',
						data: {
							user_id: this.name,
							password: this.password
						},

						success(res) {
							console.log(res)
						}
					})





				} else {
					//弹一个提示框
					uni.showModal({
						title: '提示',
						content: '请输入正确的账号和密码',
						success: function(res) {
							if (res.confirm) {
								console.log('用户点击确定');
							} else if (res.cancel) {
								console.log('用户点击取消');
							}
						}
					})
					this.checkshow = true
				}

			}
		}
	};
</script>

<style lang="scss">
	.content {
		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: center;
	}

	.top-bar {
		position: absolute;
		top: 0;
		width: 100%;
		height: 88rpx;
		padding-top: var(--status-bar-height);
		box-sizing: border-box;
		background: $uni-bg-color;
		// box-shadow: 0rpx 1rpx 0rpx 0rpx rgba(0, 0, 0, 0.1);
		margin-top: 16rpx;

		.top-bar-left {
			float: left;
			padding-left: 24rpx;
			padding-top: 20rpx;

			.back {
				width: 48rpx;
				height: 48rpx;
			}
		}

		.top-bar-right {
			float: right;
			margin-bottom: 30rpx;
			padding-right: 24rpx;
			padding-top: 20rpx;

			.close {
				width: 48rpx;
				height: 48rpx;
			}
		}
	}

	.logo {
		padding-top: 100rpx;

		.logo-image {
			width: 400rpx;
			height: 400rpx;
		}
	}

	.main {
		padding: 54rpx $uni-spacing-row-lg 120rpx;

		// .title {
		// 	width: 100%;
		// 	height: 50rpx;
		// 	text-align: center;
		// 	font-size: 56rpx;
		// 	font-family: PingFangSC-Medium, PingFang SC;
		// 	font-weight: 500;
		// 	color: rgba(39, 40, 50, 1);
		// 	line-height: 80rpx;
		// }
		.inputs {

			// padding-top: 48rpx;
			.input {
				border: none;
				height: 60rpx;
				width: 628rpx;
				font-size: 28rpx;
				font-weight: 500;
				color: $uni-text-color;
				line-height: 88rpx;
				border-bottom: 1rpx solid $uni-border-color;
			}

			.inputs-div {
				position: relative;
				padding: 20rpx;
			}

			.employ,
			.checknumber {
				position: absolute;
				top: 100rpx;
				left: 10rpx;

				margin-top: 20rpx;
				margin-left: 5rpx;

				font-size: 22rpx;
				color: #F07373;

			}

			.ishasnumber {}

			.invalid {
				position: absolute;
				right: 20rpx;
				top: 20rpx;
				float: right;
				font-size: $uni-font-size-base;
				font-family: PingFangSC-Medium, PingFang SC;
				font-weight: 500;
				color: rgba(255, 93, 91, 1);
				line-height: 40rpx;
				padding-left: 10rpx;
			}

			.show {
				position: absolute;
				right: 30rpx;
				top: 20rpx;
				width: 42rpx;
				height: 32rpx;
			}

			.ok {
				position: absolute;
				top: 20rpx;
				right: 20rpx;
				width: 42rpx;
				height: 32rpx;
			}
		}
	}

	.submit {
		margin: 0 auto;
		width: 520rpx;
		height: 96rpx;
		background: #3c7de9;
		box-shadow: 0px 25px 16px -18px #3c7de9;
		border-radius: 48rpx;
		font-size: $uni-font-size-lg;
		font-weight: 520;
		color: rgba(255, 255, 255, 1);
		line-height: 96rpx;
		text-align: center;

		&:active {
			background-color: #48689e;
		}
	}
</style>
