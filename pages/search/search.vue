<template>
	<view style="position: relative;">
		<!-- 搜索框 start -->
		<view class="search-wrapper">
			<image src="../../static/icon/search-top.png" mode=""></image>
			<input maxlength="15" type="text" @blur="clearResult" @confirm="searchMovie" confirm-type="search" value="" placeholder="请输入电影名称" />
		</view>
		<!-- 搜索框 end -->
		<!-- 推荐内容 start -->
		<view class="rcd-movie" v-if="!searchList.length">
			<view class="rcd-item" v-for="(item, index) in rcdMovies" :key="item._id">
				<navigator :url="'../detail/detail?id='+item._id">
					<image class="poster" :src="item.posterPath" mode=""></image>
					<view class="movie-name">{{item.movieName}}</view>
					<trailler-stars :showNum=1 :score="item.score" />
				</navigator>
			</view>
		</view>
		<!-- 推荐内容 end -->
		<!-- 搜索结果 start -->
		<view class="result-list" v-else>
			<view class="result-item" v-for="item in searchList" :key="item._id">
				<navigator :url="'../detail/detail?id='+item._id">
					<image :src="item.posterPath" mode=""></image>
					<view class="result-info">
						<view class="info-name">
							{{item.movieName}}
						</view>
						<view class="info-type">
							{{item.type}}
						</view>
						<view class="info-date">
							{{item.releaseDate}}
						</view>
					</view>
					<view class="result-score">
						{{item.score.toFixed(1)}}分
					</view>
				</navigator>
			</view>
		</view>
		<!-- 搜索结果 end -->
	</view>
</template>

<script>
	import traillerStars from '../../component/traillerStars/traillerStars.vue'
	export default {
		data() {
			return {
				rcdMovies: [],
				searchList: []
			}
		},
		components: {
			traillerStars // 打星星组件
		},
		onShow() {
			// 每展示一次搜索页 调用一次查询
			this.getRcdMovie()
		},
		methods: {
			// 获取推荐电影信息
			getRcdMovie() {
				uni.request({
					url: 'http://127.0.0.1:3000/random',
					success: (res) => {
						this.rcdMovies = res.data.movie
					}
				})
			},
			
			searchMovie(event) {
				let keyword = event.target.value.trim()
				if(keyword == '') {
					return false
				}
				uni.request({
					url: 'http://127.0.0.1:3000/search?keyword=' + keyword,
					success: (res) => {
						this.searchList = res.data.movie
					}
				})
			},
			clearResult(event) {
				if(event.target.value.trim() == '') {
					this.searchList = []
				}
			}
			
		}
	}
</script>

<style>
	@import url("./search.css");
</style>
