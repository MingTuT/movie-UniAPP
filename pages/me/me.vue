<template>
	<view>
		<!-- 未登录 start -->
		<view class="not-logged" v-if="!user">
			<view class="logged-button">
				<navigator url="../login/login">登录</navigator>
			</view>
		</view>
		<!-- 未登录 end -->
		<!-- 已登录 start -->
		<view class="logged" v-else>
			<view class="user-info">
				<image class="avatar" :src="user.avatar" mode="aspectFill"></image>
				<view class="user-name">{{user.nickName}}</view>
				<image class="sex" :src="user.sex?'../../static/icon/male.png':'../../static/icon/female.png'" mode=""></image>
			</view>
			<view class="user-signature">
				个性签名 : {{user.signature}}
			</view>
			<view class="settings" @click="setting">
				<image src="../../static/icon/settings.png" mode=""></image>修改资料
			</view>
			<view class="log-out" @click="logOut">
				<image src="../../static/icon/out.png" mode=""></image>退出登录
			</view>
		</view>
		<!-- 已登录 end -->
	</view>
</template>

<script>
	export default {
		data() {
			return {
				user: null
			}
		},
		created() {
			// 从session中取登录的user
			this.user = uni.getStorageSync('user')
		},
		onShow() {
			this.user = uni.getStorageSync('user')
		},
		methods: {
			logOut() {
				uni.removeStorageSync('user')
				uni.switchTab({
				    url: '/pages/index/index'
				});
			},
			setting() {
				uni.navigateTo({
				    url: '/pages/setting/setting'
				});
			}
		}
	}
</script>

<style>
	@import url("./me.css");
</style>
