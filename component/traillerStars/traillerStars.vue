<template>
	<view class="rating">
		<!-- <image src="../../static/icon/star.png" mode=""></image>
		<image src="../../static/icon/star-gray.png" mode=""></image> -->
		<image v-for="(item,index) in countStar" :key="index" src="../../static/icon/star.png" mode=""></image>
		<image v-for="(item,indey) in 5-countStar" :key="indey+'gstar'" src="../../static/icon/star-gray.png" mode="">
		</image>
		<text v-if="showNum">{{this.score.toFixed(1)}}</text>
	</view>
</template>

<script>
	export default {
		name: "traillerStars",
		data() {
			return {

			}
		},
		props: {
			score: 0,
			showNum: 0 //是否显示  1显示  0不显示
		},
		computed: {
			countStar: function() {
				return parseInt(Number(this.score) / 2)
			}

		}

	}
</script>

<style>
	.rating {
		display: flex;
		align-items: center;
	}

	.rating image {
		width: 30upx;
		height: 30upx;

	}

	.rating text {
		margin-left: 10upx;
		font-weight: 700;
		color: orange;
	}
</style>
