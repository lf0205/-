<template>
	<view class="content">
		<view class="uni-padding-wrap">
			<!-- 轮播 -->
			<view class="page-section swiper">
				<view class="page-section-spacing">
					<swiper  class="swiper" :indicator-dots="indicatorDots" :autoplay="autoplay" :interval="interval" :duration="duration">
						<swiper-item @click='swipers(i)' v-for="m,i in carousel" class="imgBox" :key='i'>
							<view class="swiper-item uni-bg-red">
								<image class="carouselImg" :src="m.imgpic_link"></image>
							</view>
						</swiper-item>
					</swiper>
				</view>
			</view>
			<!-- 歌单分类 -->
			<view class="sort">
				<view @click="recommends" class="sort-left">
					<image  mode="aspectFill" class="sort-left-recommend" :src="recommend.imgpic_link"></image>
					<p>{{recommend.title}}</p>
					<span>RECOMMEDNED</span>
					<span>DAILY</span>
					<p class='iconfont icon-weibiaoti--2'></p>
				</view>
				<view class="sort-right">
					<view class="sort-right-sort">
						<view class='sortbd'>
							<p>音乐分类</p>
							<p>MUSIC CATEGORY</p>
						</view>
					</view>
					<view class="sort-right-ranking">
						<view class='rankingbd'>
							<p>排行</p>
							<p>CHART</p>
						</view>
					</view>
					<view class="sort-right-nearby">
						<view class='nearbybd'>
							<p>附近</p>
							<p>NEARBY</p>
						</view>
					</view>
				</view>
			</view>
		</view>
		
		<!-- 推荐歌单 -->
		<SongSheetDemo/>
		
		<!-- 申请歌单 -->
		<ApplyDemo/>
		
		<!-- 原创音乐 -->
		<MusicDemo/>
		
		<!-- 翻唱音乐 -->
		<CoverDemo/>
		
		<!-- 热门音乐人 -->
		<MusicianDemo/>
	</view>
</template>

<script>
	// 导入字体图标
	import '../../static/font/iconfont.css'
	
	// 通过导入数据,获取到Easy-mock里面的数据
	export const index = 'https://www.easy-mock.com/mock/5d5dee346728653b7c6b3844/appData'
	
	// 导入其他组件
	import SongSheet from '../../components/SongSheet/SongSheet.vue'
	import Apply from '../../components/Apply/Apply.vue'
	import Music from '../../components/Music/Music.vue'
	import Cover from '../../components/Cover/Cover.vue'
	import Musician from '../../components/Musician/Musician.vue'
	
	export default {
		// 导入其他组件后需要注册才能使用
		components:{
			'SongSheetDemo':SongSheet,
			'ApplyDemo':Apply,
			'MusicDemo':Music,
			'CoverDemo':Cover,
			'MusicianDemo':Musician
		},
		data() {
			return {
				data:[],
				carousel:[],
				recommend:[],
				background: ['color1', 'color2', 'color3'],
				indicatorDots: true,
				autoplay: true,
				interval: 2000,
				duration: 500
			}
		},
		onLoad() {
			uni.request({
				url:index,
				method: 'GET',
				data: {},
				success: res => {
					console.log('app数据获取成功:',res.data)
					this.data = res.data
					this.carousel = res.data.data.shuffling
					this.recommend = res.data.data.today_recommends.cate_img
				},
				fail: () => {},
				complete: () => {}
			});
		},
		methods: {
			swipers(id){
				if(id==0){
					uni.navigateTo({
						url: './swiperinfo/swiperinfo?id='+id
					});
				}else{
					uni.navigateTo({
						url: './swiperpages/swiperpages?id='+id
					});
				}
				
				console.log(id);
			},
			recommends(){
				console.log(1);
				uni.navigateTo({
					url: './recommends/recommends'
				});
			}
		}
	}
</script>

<style>
	.uni-padding-wrap{
		margin-bottom: 10px;
	}
	.content {
		padding: 15px;
	}
	.imgBox{
		border-radius: .5rem;
	}
	.carouselImg{
		width: 100%;
		display: block;
		height: 150px;
	}
	.sort{
		margin-top: 20px;
		height: 125px;
	}
	.sort-left{
		text-shadow: 0 1px 0.04rem rgba(0,169,191,.66);
		color: #FFFFFF;
		width: 35%;
		padding: 0 10px;
		height: 100%;
		position: relative;
		float: left;
		overflow: hidden;
	}
	.sort-left>p{
		font-size: 17px;
	}
	.sort-left>span{
		font-size: 12px;
		display:block
	}
	.sort-left>p:nth-of-type(2){
		font-size: 33px;
	}
	.sort-left-recommend{
		border-radius: 5px;		
		position: absolute;
		top: 0;
		left: 0;
		z-index: -1;
		width: 100%;
		height: 100%;
	}
	.sort-right{
		text-shadow: 0 1px 0.04rem rgba(0,169,191,.66);
		float: right;
		height: 100%;
		width:55%;
		color: #FFFFFF;
	}
	.sort-right-sort{
		margin-bottom: 10px;
		width: 90%;
		height: 50%;
		background: #75ddeb url(../../static/sort.png) no-repeat 90%/3rem auto;
		border-radius: 5px;
		padding: 0 10px;
	}
	.sort-right-ranking{
		width: 35%;
		background: #f5d79d url(../../static/ranking.png) no-repeat 90%/1rem auto;
		float: left;
		padding: 0 10px;
		border-radius: 5px;
	}
	.sort-right-nearby{
		width: 35%;
		background: #8de0ce url(../../static/nearby.png) no-repeat 90%/1rem auto;
		float: right;
		padding: 0 10px;
		border-radius: 5px;
	}
	
	
</style>
