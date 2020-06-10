<template>
	<view class="detail">
		<view class="detail-title">
			我是一个前端工程师，我们要不要学 node js
		</view>
		<view class="detail-header">
			<view class="detail-header-logo">
				<image src="../../static/images/img/avatar1.jpg" mode="aspectFill"></image>
			</view>
			<view class="detail-header-content">
				<view class="detail-header-content-title">
					meHao
				</view>
				<view class="detail-header-content-info">

					<text>{{collection}} 动态</text>
					<text>{{followers}} 赞</text>
				</view>
			</view>
		</view>
		<view class="detail-content">
			xfdsf
		</view>
		<view class="detail-bottom">
			<view class="detail-bottom__input" @click="openComment">
				<text >谈谈你的看法</text>
				<uni-icons type="compose" size="16" color="#F07373"></uni-icons>
			</view>
			<view class="detail-bottom__icons">
				<view class="detail-bottom__icons-box">
					<uni-icons type="chat" size="22" color="#F07373"></uni-icons>
				</view>
				<view class="detail-bottom__icons-box">
					<uni-icons type="heart" size="22" color="#F07373"></uni-icons>
				</view>
				<view class="detail-bottom__icons-box">
					<uni-icons type="hand-thumbsup" size="22" color="#F07373"></uni-icons>
				</view>
			</view>
		</view>
		<uni-popup ref="popup" type="bottom" >
			<view class="popup-wrap">
				<view class="popup-header">
					<text class="popup-header__item" @click="close">取消 </text>
					<text class="popup-header__item" @click="close">发布 </text>
				</view>
				<view class="popup-content">
					<textarea class="popup-textarea" v-model="commentsValue" maxlength="200" fixed placeholder="请输入评论内容" />
					<view class="popup-count">{{commentValue.length}}/200</view>
				</view>
			</view>
		</uni-popup>
	</view>
</template>

<script>
	export default {
		onLoad(data) {
			this.collection=data.collection
			this.followers=data.followers
			
			
			
			
		},
		onReady() {
			
		},
		data() {
			return {
				collection:0,
				followers:0,
				commentValue:''

			}
		},
		methods: {
			openComment(){
				this.$refs.popup.open()
			},
			close(){
				// 关闭窗口清空内容 
				this.commentsValue = ''
				this.$refs.popup.close()
			},

		}
	}
</script>

<style lang="scss">
	.detail {
		padding: 15px 0;
		padding-bottom: 54px;
	}

	.detail-title {
		padding: 0 15px;
		font-size: 18px;
		font-weight: bold;
		color: #333;
	}
	.detail-header {
		display: flex;
		align-items: center;
		margin-top: 10px;
		padding: 0 15px;
	
		.detail-header-logo {
			flex-shrink: 0;
			width: 50px;
			height: 50px;
			border-radius: 50%;
			overflow: hidden;
	
			image {
				width: 100%;
				height: 100%;
			}
		}
	
		.detail-header-content {
			width: 100%;
			padding-left: 10px;
			display: flex;
			flex-direction: column;
			justify-content: space-between;
			font-size: 12px;
	
			.detail-header-content-title {
				font-size: 14px;
				color: #333;
			}
	
			.detail-header-content-info {
				color: #999;
	
				text {
					margin-right: 10px;
				}
			}
		}
		}
	.detail-content {
		margin-top: 20px;
		min-height: 500px;}
	.detail-bottom {
			position: fixed;
			bottom: 0;
			left: 0;
			display: flex;
			align-items: center;
			width: 100%;
			height: 44px;
			border-top: 1px #f5f5f5 solid;
			background-color: #fff;
			box-sizing: border-box;
		
			.detail-bottom__input {
				display: flex;
				justify-content: space-between;
				align-items: center;
				margin-left: 10px;
				padding: 0 10px;
				width: 100%;
				height: 30px;
				border: 1px #ddd solid;
				border-radius: 5px;
		
				text {
					font-size: 14px;
					color: #999;
				}
			}
		
			.detail-bottom__icons {
				display: flex;
				flex-shrink: 0;
				padding: 0 10px;
		
				.detail-bottom__icons-box {
					position: relative;
					display: flex;
					align-items: center;
					justify-content: center;
					width: 44px;
				}
			}
		}
	
	.popup-wrap {
			background-color: #fff;
			.popup-header {
				display: flex;
				justify-content: space-between;
				font-size: 14px;
				color: #666;
				border-bottom: 1px #F5F5F5 solid;
				.popup-header__item {
					height: 50px;
					line-height: 50px;
					padding: 0 15px;
				}
			}
			.popup-content {
				width: 100%;
				padding: 15px;
				box-sizing: border-box;
				.popup-textarea {
					width: 100%;
					height: 200px;
					
				}
				.popup-count {
					display: flex;
					justify-content: flex-end;
					font-size: 12px;
					color: #999;
				}
			}
		}	
		
		
</style>
