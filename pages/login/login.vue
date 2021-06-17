<template>
	<view>
		<view class="bg"></view>
		<view class="login-form">
			<form action="">
				<view class="login-item">
					<image src="../../static/icon/email.png" mode=""></image>
					<input type="text" value="" placeholder="请输入邮箱" />
				</view>
				<view class="login-item">
					<image src="../../static/icon/password.png" mode=""></image>
					<input type="password" value="" placeholder="请输入邮箱" />
				</view>
				<view class="register">
					<navigator url="../register/register">还未拥有账号？</navigator>
				</view>
				<view class="login-err">
					邮箱或密码错误
				</view>
				<button type="default">登录</button>
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
			
		}
	}
</script>

<style>
	@import url("./login.css");
</style>
