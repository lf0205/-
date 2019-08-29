<template>
	<view class="CoverMusic">
		<view class='CoverMusicTitle'>
			<view class='CoverMusicTitleLogo'>
				<h2>翻唱音乐</h2>
				<p></p>
			</view>
		</view>
		<view class="CoverMusicList">
			<ul>
				<li class='CoverMusicListBox' v-for='(m,i) in CoverMusicData' :key='i'>
					<view class='CoverMusicListImg'>
						<image :src="m.imgpic_link" mode=""></image>
						<p>{{CMusic.title}}</p>
					</view>
					<view class='CoverMusicListInfo'>
						<h2>{{m.title}}</h2>
						<p>{{m.nickname}}</p>
						<span class='iconfont icon-headset'>{{m.counts}}</span>
						<view class='CoverMusicListMv' v-if='m.mv'>MV</view>
					</view>
				</li>
			</ul>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				CoverMusicData:[],
				CMusic:[]
			}
		},
		methods: {
			
		},
		mounted() {
			uni.request({
				url: 'https://www.easy-mock.com/mock/5d5e6c69d220c910f27ece02/api2/api2',
				method: 'GET',
				data: {},
				success: res => {
					console.log('翻唱音乐',res.data.data.type_music[1].music)
					this.CoverMusicData = res.data.data.type_music[1].music
					this.CMusic = res.data.data.type_music[1]
				},
				fail: () => {},
				complete: () => {}
			});
		}
	}
</script>

<style>
.CoverMusicTitle{
	background: url(../../static/ace03.png) no-repeat;
	background-size: auto 2rem;
	display: flex;
	align-items: center;
	background-position: 0;
	height: 62px;
	padding-left: 40px;
}
.CoverMusicTitleLogo{
	position: relative;
	display: inline-block;
}
.CoverMusicTitleLogo>h2{
	font-size:17px;
}
.CoverMusicTitleLogo>p{
	position: absolute;
	bottom: 3px;
	right: 0;
	width: 44px;
	height: 8px;
	border-radius: 5px;
	background: #ffd9e6;
	z-index: -1;
}
.CoverMusicList>ul{
	overflow:hidden;
	list-style:none;
	padding:0;
}
.CoverMusicListBox{
	border-radius:5px;
	border:1px solid #ccc;
	margin-bottom:5px;
	display:flex;
	/* width:345px; */
	height:75px;
}
.CoverMusicListImg{
	position:relative;
	overflow:hidden;
	display:inline-block;
	width:75px;
	height:75px;
}
.CoverMusicListImg>image{
	border-radius:5px 0 0 5px;
	display:inline-block;
	width:100%;
	height:100%;
}
.CoverMusicListImg>p{
	position:absolute;
	top:0;
	right:0;
	width: 30px;
	padding:0 3px;
	background: #ff6699;
	color: #fff;
	border-radius: 0 0 0 5px;
	line-height: 20px;
	font-size: 12px;
	text-align: center;
}
.CoverMusicListInfo{
	position:relative;
	flex:1;
	padding:5px 10px;
	background:#efefef;
	display:inline-block;
}
.CoverMusicListInfo>h2{
	font-size:13px;
	color:#000;
}
.CoverMusicListInfo>p{
	font-size:14px;
	color:#9DA2A6;
}
.CoverMusicListInfo>span{
	font-size:12px;
	color:#9DA2A6;
}
.CoverMusicListMv{
	position:absolute;
	right:10px;
	top:10px;
	width:25px;
	text-align: center;
	font-family: Arial;
	font-size:12px;
	line-height:18px;
	border-radius:5px;
	background:#bfbfbf;
	color:#fff;
}
</style>
