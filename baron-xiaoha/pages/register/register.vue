<template>
	<view class="content">
		<!-- 顶栏 -->
		<view class="top-bar">
			<view class="top-bar-left" @click="goLogin"><image class="back" src="../../static/images/register/back.png"></image></view>
		</view>
		<!-- 图标 -->
		<view class="logo"><image src="../../static/images/index/logo.png" class="logo-image"></image></view>
		<!-- 登陆 -->
		<view class="main">
			<view class="title"></view>
			<view class="inputs">
				<view class="inputs-div">
					<input class="input" type="text" placeholder="请输入用户名" placeholder-style="color:#aaa;font-weight:400;" @blur="isname" v-model="name" />
					<view class="employ" v-show="employ">已占用</view>
					<image src="../../static/images/register/right.png" class="ok" v-show="isuser"></image>
				</view>
				<view class="inputs-div">
					<input class="input" type="text" placeholder="请输入邮箱" placeholder-style="color:#aaa;font-weight:400;" @blur="ismail" v-model="email" />
					<view class="employ" v-show="employ">已占用</view>
					<view class="invalid" v-show="invalid">邮箱无效</view>
					<image src="../../static/images/register/right.png" class="ok" v-show="isemail"></image>
				</view>
				<view class="inputs-div">
					<input class="input" :type="type" placeholder="请设置密码" placeholder-style="color:#aaa;font-weight:400;" />
					<view class="employ" v-show="employ">已占用</view>
					<image :src="showurl" class="show" @tap="showon"></image>
				</view>
				<view class="inputs-div">
					<input class="input" :type="type" placeholder="请确认密码" placeholder-style="color:#aaa;font-weight:400;" />
					<view class="employ" v-show="employ">已占用</view>
					<image :src="showurl" class="show" @tap="showon"></image>
				</view>
			</view>
		</view>
		<!-- 登陆按钮 -->
		<view class="submit">注册</view>
	</view>
</template>

<script>
export default {
	data() {
		return {
			type: 'password',
			isuser: 0, //用户名是否占用
			isemail: 0, //邮箱是否占位
			show: false, // 是否显示密码
			invalid: false, // 邮箱是否符合
			employ: false, //是否被占用
			showurl: '../../static/images/register/showin.png',
			email: '',
			name: ''
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
			right: 20rpx;
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
