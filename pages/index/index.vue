<template>
	<view class="content">
		<image class="logo" src="../../static/2411587701112_.pic.png"></image>
		<view class="text-area">
			<view class="title">账号</view>
			<input class="uni-input" type="text" placeholder="请输入手机号" v-model="username" />
		</view>
		<view class="text-area">
			<view class="title">密码</view>
			<input class="uni-input" password type="text" placeholder="请输入密码" v-model="password" />
		</view>
		<view class="text">
			<text @click="noPassword()">忘记密码</text>
		</view>
		<view class="buttons">
			<button style="color: #FFFFFF;
		background-color: #00A2FF;" @click="GOhonme">立即登录</button>
		</view>
		<view class="zhuce">
			<view style="margin-bottom: 80rpx;box-sizing: border-box;" @click="goRetrieve()">去注册</view>
			<view style="color: #999999;">其他方式登录</view>
			<button class="button" style="margin-top: 40rpx;box-sizing: border-box;display: flex;align-items: center;justify-content: center;background-color: #fff;border: none !important;" open-type="getUserInfo" lang="zh_CN"
			 @getuserinfo="appLoginWx">
				<image src="../../static/wxdl.png" mode="" style="width: 90rpx;height: 90rpx;"></image>
			</button>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				username: '15652653114',
				password: '123456'

			}
		},
		onLoad() {

		},
		methods: {
			GOhonme() {

				// uni.navigateTo({
				// 	url: './one'
				// });
				uni.switchTab({
					url: './one'
				});
				console.log('小贤')


			},
			appLoginWx() {
				// #ifdef MP-WEIXIN
				uni.getProvider({
					service: 'oauth',
					success: function(res) {
						console.log(res)
						if (~res.provider.indexOf('weixin')) {
							uni.login({
								provider: 'weixin',
								success: (res) => {
									console.log(res);
									uni.getUserInfo({
										provider: 'weixin',
										success: (info) => { //这里请求接口

											// console.log(info.userInfo);
											// uni.setStorageSync('nemess', JSON.stringify(info.userInfo));
											uni.setStorage({
											    key: 'nemess',
											    data: JSON.stringify(info.userInfo),
											    success: function () {
											        console.log('success');
											    }
											});
											uni.switchTab({
												url: './one'
											});

										},
										fail: () => {
											uni.showToast({
												title: "微信登录授权失败",
												icon: "none"
											});
										}
									})

								},
								fail: () => {
									uni.showToast({
										title: "微信登录授权失败",
										icon: "none"
									});
								}
							})

						} else {
							uni.showToast({
								title: '请先安装微信或升级版本',
								icon: "none"
							});
						}
					}
				});
				//#endif

			},


			// console.log('微信授权')
		},
		goRetrieve() {
			// uni.navigateTo({
			// 	url:"../register/register"
			// })
			console.log('sss')
		},
		noPassword() {
			// uni.navigateTo({
			// 	url:"../retrieve/retrieve"
			// })
			console.log('sss')
		}

	}
</script>

<style>
	
.button::after{ border: none; }	
	.content {
		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: center;
		padding: 100rpx 90rpx 0 90rpx;
		box-sizing: border-box;
	}

	.logo {
		height: 145rpx;
		width: 145rpx;
		/* margin-top: 318rpx; */
		margin-left: auto;
		margin-right: auto;
		margin-bottom: 50rpx;
		box-sizing: border-box;
	}

	.text-area {
		display: flex;
		width: 100%;
		/* padding-left: 106rpx; */
		padding: 40rpx 0 20px 0;
		box-sizing: border-box;
		font-size: 28rpx;
		border-bottom: rgba(51, 51, 51, 0.06) 1rpx solid;

		/* justify-content: center; */
	}

	.title {
		font-size: 28rpx;
		color: #999999;
		padding-right: 30rpx;
		box-sizing: border-box;
	}

	.uni-input {
		width: 80%;
		font-size: 28rpx;
		color: #999999;
		box-sizing: border-box;
	}

	.text {
		padding: 30rpx 0;
		color: #ccc;
		font-size: 28rpx;
		display: flex;
		width: 100%;
		justify-content: flex-end;
		box-sizing: border-box;
	}

	.buttons {
		width: 100%;

	}

	.zhuce {
		width: 100%;
		text-align: center;
		color: #00A2FF;
		font-size: 32rpx;
		margin-top: 30rpx;
		box-sizing: border-box;
	}
</style>
