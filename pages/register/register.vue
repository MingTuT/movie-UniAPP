<template>
	<view>
		<view class="bg"></view>
		<!-- 注册表单 start -->
		<view class="reg-form">
			<form action="">
				<view class="reg-item">
					<image src="../../static/icon/email.png" mode=""></image>
					<input type="text" value="" placeholder="请输入可用的邮箱" />
				</view>
				<view class="email-err">
					*邮箱错误
				</view>
				<view class="reg-item">
					<image src="../../static/icon/password.png" mode=""></image>
					<input type="password" value="" placeholder="请输入5-10位的英文或数字" />	
				</view>
				<view class="pwd-err">
					*密码格式错误
				</view>
				<view class="reg-item">
					<image src="../../static/icon/confirm.png" mode=""></image>
					<input type="password" value="" placeholder="请再次输入密码" />
				</view>
				<view class="pwds-err">
					*两次密码不一致
				</view>
				<!-- <view class="reg-item">
					<image src="../../static/icon/password.png" mode=""></image>
					<input type="text" value="1" />
				</view>
				<view class="reg-item">
					<image src="../../static/icon/confirm.png" mode=""></image>
					<input type="text" value="1" />
				</view>
				<button type="default">注册</button> -->
				<button type="default">注册</button>
			</form>
		</view>
		<!-- 注册表单 end -->
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
	@import url("./register.css");
</style>
