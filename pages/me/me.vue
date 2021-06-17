<template>
	<view>
		<!-- 未登录 start -->
		<view class="not-logged" v-if="false">
			<view class="logged-button">
				登录
			</view>
		</view>
		<!-- 未登录 end -->
		<!-- 已登录 start -->
		<view class="logged">
			<view class="user-info">
				<image class="avatar" src="../../static/img/3.webp" mode="aspectFill"></image>
				<view class="user-name">西红柿炒鸡蛋</view>
				<image class="sex" src="../../static/icon/female.png" mode=""></image>
			</view>
			<view class="user-signature">
				个性签名 : 不爱吃土豆🥔
			</view>
			<view class="settings">
				<image src="../../static/icon/settings.png" mode=""></image>修改个人信息
			</view>
			<view class="log-out">
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
				
			}
		},
		methods: {
			
		}
	}
</script>

<style>
	@import url("./me.css");
</style>
