<template>
	<view>
		<view class="bg"></view>
		<view class="login-form">
			<form @submit="login">
				<view class="login-item">
					<image src="../../static/icon/email.png" mode=""></image>
					<input type="text" value="" placeholder="请输入邮箱" name="email" />
				</view>
				<view class="login-item">
					<image src="../../static/icon/password.png" mode=""></image>
					<input type="password" value="" placeholder="请输入密码" name="password" />
				</view>
				<view class="register">
					<navigator url="../register/register">还未拥有账号？</navigator>
				</view>
				<view class="login-err">
					邮箱或密码错误
				</view>
				<button form-type="submit" type="default">登录</button>
			</form>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				
			}
		},
		methods: {
			login(e) {
				let email = e.detail.value.email
				let password = e.detail.value.password
				
				if(email && password) {
					uni.request({
						url: 'http://127.0.0.1:3000/login',
						method: 'POST',
						data: {
							email,
							password
						},
						success: (res) => {
							let msg_code = res.data.msg_code
							if(msg_code) {
								uni.setStorageSync('user', res.data.user);
								uni.switchTab({
								    url: '/pages/me/me'
								});
							}else {
								uni.showToast({
								    title: '账号或密码错误',
								    duration: 2000,
									icon: "none"
								});
							}
						}
					})	
				}else {
					uni.showToast({
					    title: '请填写账号密码',
					    duration: 2000,
						icon: "none"
					});
				}
				
			}
		}
	}
</script>

<style>
	@import url("./login.css");
</style>
