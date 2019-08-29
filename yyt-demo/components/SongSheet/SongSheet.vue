<template>
	<view class="SongSheet">
		<view class='SongSheetTitle'>
			<view class="SongSheetTitleBox">
				<h2>{{Songtitle}}</h2>
				<p></p>
			</view>
		</view>
		<view class="Songs">
			<view class='SongsBox' v-for="(s,i) in song" :key='i'>
				<view class='SongsImgBox'>
					<image class="SongImg" :src="s.imgpic_link"></image>
					<p class='iconfont icon-headset'>{{s.counts}}</p>
				</view>
				<p>{{s.title}}</p>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				song:[],
				Songtitle:'推荐歌单'
			}
		},
		methods: {
			
		},
		mounted(){
			uni.request({
				url: 'https://www.easy-mock.com/mock/5d5dee346728653b7c6b3844/appData',
				method: 'GET',
				data: {},
				success: res => {
					this.song = res.data.data.recommend_song.song
					console.log("推荐歌单数据获取成功:",res.data.data.recommend_song.song)
				},
				fail: () => {},
				complete: () => {}
			});
		}
	}
</script>

<style>
	.SongSheet{
		overflow: hidden;
	}
	.SongSheetTitle{
		height: 62px;
		padding-left: 40px;
		background: url(../../static/ace04.png)no-repeat;
		background-size: auto 2rem;
		display: flex;
		align-items: center;
		background-position: 0;
	}
	.SongSheetTitle>.SongSheetTitleBox{
			position: relative;
			display: inline-block;
	}
	.SongSheetTitle>.SongSheetTitleBox>h2{
		color: #2b2b2b;
		font-size: 17px;
	}
	.SongSheetTitle>.SongSheetTitleBox>p{
		position: absolute;
		bottom: 3px;
		right: 0;
		width: 44px;
		height: 6.5px;
		border-radius: 5px;
		background: #ffd9e6;
		z-index: -1;
	}
	.SongsBox{
		margin-bottom: 5px;
		width:107.5px;
		height: 139px;
	}
	.SongsBox>p{
		font-size: 13px;
	}
	.Songs{
		display: flex;
		justify-content: space-between;
		flex-wrap: wrap;
	}
	.SongsImgBox{
		width:94px;
		padding-right: 12px;
		height: 94px;
		background: url(../../static/cj.png) no-repeat 100%;
		background-size: .64rem 100%;
		position: relative;
	}
	.SongsImgBox::after{
		content: "";
		display: block;
		width: 100%;
		height: 100%;
		position: absolute;
		z-index: 5;
		background-size: 100% 100%;
		bottom:0;
		background:url(../../static/bd.png);
	}
	.SongsImgBox>p{
		position: absolute;
		bottom: 0;
		right: 20px;
		color: #FFFDEF;
		font-size: 12px;
		z-index: 2;
	}
	.SongImg{
		border: 1px solid #EEEEEE;
		border-radius: 5px;
		width: 100%;
		height: 100%;
	}
</style>
