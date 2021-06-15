<template>
	<view class="content">
		<!-- 轮播图 start -->
		<swiper class="swiper" circular="true" indicator-dots="true" autoplay="true" interval="5000" duration="1500">
			<swiper-item v-for="(item, index) in carouselList" :key="index">
				<navigator :url="'../detail/detail?id='+item.movieId">
					<image :src="item.imgPath" mode="aspectFill"></image>
				</navigator>
			</swiper-item>
		</swiper>
		<!-- 轮播图 end -->
		<!-- 热门视频 start -->
		<view class="popular-movie">
			<view class="popular-title">
				<image src="../../static/icon/popular.png" mode=""></image>
				<view class="title-text">热门视频</view>
			</view>
			<scroll-view scroll-x="true">
				<view class="scroll-wrapper">
					<view v-for="(item, index) in hotList" :key="item._id" class="popular-item">
						<navigator :url="'../detail/detail?id='+item.movieId">
							<image class="poster" :src="item.posterPath" mode=""></image>
							<text class="movie-name">{{item.movieName}}</text>
							<trailler-stars :showNum=1 :score="item.score" />
						</navigator>
					</view>
				</view>
			</scroll-view>
		</view>
		<!-- 热门视频 end -->
		<!-- 口碑电影 start -->
		<view class="high-list">
			<view class="popular-title">
				<image src="../../static/icon/trailer-icon.png" mode=""></image>
				<view class="title-text">口碑电影</view>
			</view>
			<view class="high-movie">
				<view class="high-bd">口碑榜单</view>
				<view v-for="(item,index) in niceList" :key="item._id" class="high-item">
					<navigator :url="'../detail/detail?id='+item.movieId">
						<image :src="item.posterPath" mode=""></image>
						<view class="item-wrapper">
							<view>{{item.movieName}}</view>
							<trailler-stars :showNum=1 :score="item.score" />
						</view>
					</navigator>

				</view>

			</view>
		</view>
		<!-- 口碑电影 end -->
		<!-- 推荐电影 start -->
		<view class="recommend-movie">
			<view class="popular-title">
				<image src="../../static/icon/recommend.png" mode=""></image>
				<view class="title-text">推荐电影</view>
			</view>

			<view v-for="(item, index) in recommendList" :key="item._id" class="introduction">
				<navigator :url="'../detail/detail?id='+item.movieId">
				<view class="introduction-poster">
					<image :src="item.posterPath" mode=""></image>
				</view>
				<view class="introduction-content">
					<view class="content-name">{{item.movieName}}</view>
					<view class="content-text">
						{{item.brief}}
					</view>
				</view>
				</navigator>
			</view>

		</view>
		<!-- 推荐电影 end -->



	</view>
</template>

<script>
	import traillerStars from '../../component/traillerStars/traillerStars.vue'
	export default {
		data() {
			return {
				carouselList: [], // 轮播图数据
				hotList: [],
				niceList: [],
				recommendList: []
			}
		},
		components: {
			traillerStars // 打星星组件
		},
		created() {
			this.getCarousel()
			this.getHot()
			this.getNice()
			this.getRecommend()
		},
		methods: {
			// 获取轮播图数据
			getCarousel() {
				uni.request({
					url: 'http://127.0.0.1:3000/carousel',
					success: (res) => {
						this.carouselList = res.data.carousel
					}
				});
			},
			// 获取热门视频数据
			getHot() {
				uni.request({
					url: 'http://127.0.0.1:3000/hot',
					success: (res) => {
						this.hotList = res.data.hotMovie
					}
				});
			},
			// 获取口碑榜单数据
			getNice() {
				uni.request({
					url: 'http://127.0.0.1:3000/nice',
					success: (res) => {
						this.niceList = res.data.niceMovie
					}
				});
			},
			// 获取推荐电影数据
			getRecommend() {
				uni.request({
					url: 'http://127.0.0.1:3000/recommend',
					success: (res) => {
						this.recommendList = res.data.recommendMovie
					}
				});
			}



		}
	}
</script>

<style>
	@import url("./index.css");
</style>
