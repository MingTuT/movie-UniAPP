<template>
	<view id="detail">
		<!-- 电影信息 start -->
		<view class="movie-info">
			<view class="info-lef">
				<image :src="movie.posterPath" mode=""></image>
			</view>
			<view class="info-right">
				<view class="movie-name">
					{{movie.movieName}}
				</view>
				<view class="type">
					类型：{{movie.type}}
				</view>
				<view class="language">
					语言：{{movie.language}}
				</view>
				<view class=" ">
					上映日期：{{movie.releaseDate}}
				</view>
			</view>
		</view>
		<!-- 电影信息 end -->
		<!-- 电影评分 start -->
		<view class="rating">
			<view class="rating-text">
				电影评分™
			</view>
			<view class="rating-num">
				<view>{{movie.score}} 分</view>
				<trailler-stars v-if="movie.score" :showNum=0 :score="movie.score" />
			</view>
		</view>
		<!-- 电影评分 end -->
		<!-- 简介 start -->
		<view class="brief">
			<view class="brief-title">简介</view>
			<view class="brief-content">
				{{movie.brief}}
			</view>
		</view>
		<!-- 简介 end -->
		<!-- 预告 start -->
		<view class="trailer">
			<view class="trailer-title">预告</view>
			<!-- <video :src="movie.trailer[0]" 
				:poster="movie.trailer[1]" controls></video> -->

			<video v-if="movie.trailer" :src="movie.trailer[0]" :poster="movie.trailer[1]" controls></video>

		</view>
		<!-- 预告 end -->
		<!-- 剧照 start -->
		<view class="related-pic">
			<view class="related-pic-title">剧照</view>
			<scroll-view scroll-x="true">
				<view class="scroll-wrapper">
					<view v-for="(item,index) in movie.relatedPic" :key="item._id" class="scroll-item">
						<image :src="item" mode="heightFix" @click="preImg(index)"></image>
					</view>
				</view>
			</scroll-view>
		</view>
		<!-- 剧照 end -->
	</view>
</template>

<script>
	import traillerStars from '../../component/traillerStars/traillerStars.vue'

	export default {
		data() {
			return {
				movieId: '',
				movie: {}
			}
		},
		components: {
			traillerStars // 打星星组件
		},
		onLoad(option) {
			this.movieId = option.id
			this.getMovie(this.movieId)
			// console.log(this.movieId)
		},
		created() {

		},
		methods: {
			// 获取电影详情信息
			getMovie(id) {
				uni.request({
					url: 'http://127.0.0.1:3000/movie?id=' + id,
					success: (res) => {
						res.data.movie.score = res.data.movie.score.toFixed(1)
						this.movie = res.data.movie
						// console.log(this.movie.relatedPic)
					}
				})
			},
			// 预览剧照图片
			preImg(index) {
				uni.previewImage({
					// 剧照数组
					urls: this.movie.relatedPic,
					current: index
				})


			}


		}
	}
</script>

<style>
	@import url("./detail.css");
</style>
