<template>
	<view>
		<form @submit="settingInfo">
			<view class="setting-form">
				<!-- 头像部分 start -->
				<view class="avatar">
					<image :src="avatar" mode="aspectFill" @click="changeAvatar"></image>
					<view class="">
						点击修改头像
					</view>
				</view>
				<!-- 头像部分 end -->
				<!-- 用户资料 start -->
				<view class="user-info">
					<view class="info-wrapper">
						<view class="text">
							用户名
						</view>
						<input type="text" :value="user.nickName" name="nickName" />
					</view>
					<view class="info-wrapper">
						<view class="text">
							性别
						</view>
						<picker mode="selector" :range="sex" @change="sexPicker" :value="sexValue">
							<view>{{sex[sexValue]}}</view>
						</picker>
					</view>
					<view class="info-wrapper">
						<view class="text">
							个性签名
						</view>
						<input type="text" :value="user.signature" name="signature" />
					</view>
				</view>
				<!-- 用户资料 end -->
				<button form-type="submit">保存修改</button>
			</view>
		</form>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				user: null,
				sex: ['女', '男'],
				sexValue: 1,
				avatar: '',
				// 判断头像是否有变化
				avatarFlag: false
			}
		},
		created() {
			this.user = uni.getStorageSync('user')
			this.sexValue = this.user.sex
			this.avatar = this.user.avatar
		},
		methods: {
			sexPicker(e) {
				this.sexValue = e.detail.value
			},
			// 修改头像
			changeAvatar() {
				uni.chooseImage({
				    count: 1, //默认9
				    sizeType: ['original', 'compressed'], //可以指定是原图还是压缩图，默认二者都有
				    sourceType: ['album'], //从相册选择
				    success: (res) => {
						// console.log(res.tempFilePaths)
						this.avatar = res.tempFilePaths[0]	
						this.avatarFlag = true
				    }
				});				
			},
			// 上传user信息
			settingInfo(e) {
				let _id = this.user._id
				let {nickName, signature} = e.detail.value
				let sex = this.sexValue
				let avatar = this.avatar
				let avatarFlag = this.avatarFlag
				
				if(avatarFlag) {
					uni.uploadFile({
						url: 'http://127.0.0.1:3000/setting',
						filePath: avatar,
						formData: {
							'_id': _id,
							'nickName': nickName,
							'sex': sex,
							'signature': signature
						},
						success: function (res) {
							let data = JSON.parse(res.data)
							uni.setStorageSync('user', data.user);
							uni.switchTab({
							    url: '/pages/me/me'
							});
						}
					})
				}else {
					uni.request({
						url: 'http://127.0.0.1:3000/setting',
						method: 'POST',
						data: {
							'_id': _id,
							'nickName': nickName,
							'sex': sex,
							'signature': signature
						},
						success: (res) => {
							let user = res.data.user
							uni.setStorageSync('user', user);
							uni.switchTab({
							    url: '/pages/me/me'
							});
						}
					})
				}
				
			}
			
			
		}
	}
</script>

<style>
	@import url("./setting.css");
</style>
