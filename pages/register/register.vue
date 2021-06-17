<template>
	<view>
		<view class="bg"></view>
		<!-- 注册表单 start -->
		<view class="reg-form">
			<form @submit="register">
				<view class="reg-item">
					<image src="../../static/icon/email.png" mode=""></image>
					<input @blur="checkEmail" type="text" value="" name="email" placeholder="请输入可用的邮箱" />
				</view>
				<view class="email-err" :class="{visible: emailErr}">
					*邮箱错误
				</view>
				<view class="reg-item">
					<image src="../../static/icon/password.png" mode=""></image>
					<input @blur="checkPwd" type="password" value="" name="password" placeholder="请输入5-12位的英文或数字" />
				</view>
				<view class="pwd-err" :class="{visible: pwdErr}">
					*密码格式错误
				</view>
				<view class="reg-item">
					<image src="../../static/icon/confirm.png" mode=""></image>
					<input @blur="checkPwd2" type="password" value="" name="password2" placeholder="请再次输入密码" />
				</view>
				<view class="pwds-err" :class="{visible: pwdErr2}">
					*两次密码不一致
				</view>
				<button form-type="submit" type="default">注册</button>
			</form>
		</view>
		<!-- 注册表单 end -->
	</view>
</template>

<script>
	export default {
		data() {
			return {
				password: "",
				// Flag 判断注册条件是否合格
				emailFlag: false,
				pwdFlag: false,
				pwdFlag2: false,
				// Err 是否显示错误信息
				emailErr: false,
				pwdErr: false,
				pwdErr2: false
			}
		},
		methods: {
			register(e) {
				if(this.emailFlag && this.pwdFlag && this.pwdFlag2) {
					let email = e.detail.value.email
					let password = e.detail.value.password
					uni.request({
						url: 'http://127.0.0.1:3000/register',
						method: 'POST',
						data: {
							email,
							password
						},
						success: (res) => {
							let user = res.data.user
							uni.setStorageSync('user', user);
							// console.log(uni.getStorageSync('user'))
							uni.switchTab({
							    url: '/pages/me/me'
							});
						}
					})
				}else {
					uni.showToast({
					    title: '注册信息有误',
					    duration: 2000,
						icon: "none"
					});
				}
				
			},
			checkEmail(e) {
				let email = e.target.value
				// console.log(this.emailFlag)
				let regexp = /^([a-zA-Z]|[0-9])(\w|\-)+@[a-zA-Z0-9]+\.([a-zA-Z]{2,4})$/
				this.emailFlag = regexp.test(email)
				this.emailErr = !regexp.test(email)
			},
			checkPwd(e) {
				let pwd = e.target.value
				this.password = pwd
				let regexp = /^(?![0-9]+$)(?![a-zA-Z]+$)[0-9A-Za-z]{5,12}$/
				this.pwdFlag = regexp.test(pwd)
				this.pwdErr = !regexp.test(pwd)
			},
			checkPwd2(e) {
				if (this.password == e.target.value) {
					this.pwdFlag2 = true
					this.pwdErr2 = false
				} else {
					this.pwdFlag2 = false
					this.pwdErr2 = true
				}
			}



		}
	}
</script>

<style>
	@import url("./register.css");
</style>
