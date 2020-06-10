<template>
	<view class="content">
		<!-- 顶栏 -->
		<view class="top-bar">
			<view class="top-bar-left" @click="toRegister()"><view class="text">注册</view></view>
		</view>
		<!-- 图标 -->
		<view class="logo"><image src="https://vkceyugu.cdn.bspapp.com/VKCEYUGU-baron-xiaoha/a81c29e0-a7a2-11ea-b244-a9f5e5565f30.png" class="logo-image"></image></view>
		<!-- 登陆 -->
		<view class="main">
			<view class="title"></view>
			<view class="slogan">您好，欢迎来到 小哈职友！</view>
			<view class="inputs">
				<input class="input" type="text" placeholder="用户名/邮箱" placeholder-style="color:#aaa;font-weight:400;" v-model="user" @blur="getUser" />
				<input class="input" type="text" placeholder="密码" placeholder-style="color:#aaa;font-weight:400;" password="true" v-model="password" @blur="getPwd" />
			</view>
			<view class="tips" v-show="login">输入用户名或密码错误！</view>
		</view>
		<!-- 登陆按钮 -->
		<view class="submit" @click="onlogin">登陆</view>
	</view>
</template>

<script>
import { mapState } from 'vuex';
export default {
	data() {
		return {
			login: false,
			user: '',
			password: ''
		};
	},
	onLoad() {},
	methods: {
		//跳转到注册页面
		toRegister: function() {
			uni.navigateTo({
				url: '../register/register'
			});
		},
		getUser() {
			console.log(this.user);
		},
		getPwd() {
			console.log(this.password);
		},
		onlogin() {
			if (this.user && this.password) {
				uniCloud
					.callFunction({
						name: 'login',
						data: {
							user_id: this.user,
							password: this.password
						}
					})
					.then(res => {
						console.log(res);
						console.log(res.result.status);
						if (res.result.status === 0) {
							const userId = this.user;
							uni.switchTab({
								url: '/pages/home/home',
								success() {
									uni.setStorage({
										key: 'token',
										data: 'ok'
									});
									uni.setStorage({
										key: 'user_id',
										data: userId
									});
								}
							});
							console.log(res.result);
							this.$store.commit('setUser_id', this.user);
						} else {
							console.log('登陆失败');
						}
					});
			} else {
				this.login = true;
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
	box-sizing: border-box;
	background: $uni-bg-color;
	// box-shadow: 0rpx 1rpx 0rpx 0rpx rgba(0, 0, 0, 0.1);
	.top-bar-left {
		float: left;
		margin-left: 50rpx;
		.text {
			font-size: 36rpx;
			font-family: PingFangSC-Medium, PingFang SC;
			font-weight: 510;
			color: rgba(51, 51, 51, 1);
			line-height: 88rpx;
			padding-right: 56rpx;
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
	width: 100%;
	padding-left: 120rpx;
	padding-bottom: 200rpx;
	.title {
		font-size: 56rpx;
		font-family: PingFangSC-Medium, PingFang SC;
		font-weight: 500;
		color: rgba(39, 40, 50, 1);
		line-height: 80rpx;
	}
	.slogan {
		text-align: center;
		padding-right: 90rpx;
		font-size: $uni-font-size-lg;
		font-family: PingFangSC-Regular, PingFang SC;
		font-weight: 400;
		color: #32373f;
		line-height: 56rpx;
	}
	.inputs {
		padding-top: 48rpx;
		.input {
			height: 88rpx;
			width: 628rpx;
			font-size: $uni-font-size-lg;
			font-weight: 500;
			color: $uni-text-color;
			line-height: 88rpx;
			border-bottom: 0.2rpx solid $uni-border-color;
		}
	}
	.tips {
		float: left;
		font-size: $uni-font-size-lg;
		color: $uni-color-warning;
		line-height: 56rpx;
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
