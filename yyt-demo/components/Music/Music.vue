<template>
	<view class="Music">
		<view class='MusicTitle'>
			<view class='MusicTitleLogo'>
				<h2>原创音乐</h2>
				<p></p>
			</view>
		</view>
		<view class="MusicList">
			<ul>
				<li class='MusicListBox' v-for='(m,i) in MusicData' :key='i'>
					<view class='MusicListImg'>
						<image :src="m.imgpic_link" mode=""></image>
						<p>{{Music.title}}</p>
					</view>
					<view class='MusicListInfo'>
						<h2>{{m.title}}</h2>
						<p>{{m.nickname}}</p>
						<span class='iconfont icon-headset'>{{m.counts}}</span>
						<view class='MusicListMv' v-if='m.mv'>MV</view>
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
				MusicData:[],
				Music:[]
			}
		},
		methods: {
			
		},
		mounted() {
			uni.request({
				url: 'https://www.easy-mock.com/mock/5d5e512adfc6562118918a97/api/yytdata',
				method: 'GET',
				data: {},
				success: res => {
					console.log('原创音乐',res.data)
					this.MusicData = res.data.data.type_music[0].music
					this.Music = res.data.data.type_music[0]
				},
				fail: () => {},
				complete: () => {}
			});
		}
	}
</script>

<style>
.MusicTitle{
	background: url(../../static/ace03.png) no-repeat;
	background-size: auto 2rem;
	display: flex;
	align-items: center;
	background-position: 0;
	height: 62px;
	padding-left: 40px;
}
.MusicTitleLogo{
	position: relative;
	display: inline-block;
}
.MusicTitleLogo>h2{
	font-size:17px;
}
.MusicTitleLogo>p{
	position: absolute;
	bottom: 3px;
	right: 0;
	width: 44px;
	height: 8px;
	border-radius: 5px;
	background: #ffd9e6;
	z-index: -1;
}
.MusicList>ul{
	overflow: hidden;
	list-style:none;
	padding:0;
}
.MusicListBox{
	border-radius:5px;
	border:1px solid #ccc;
	margin-bottom:5px;
	display:flex;
	/* width:345px; */
	height:75px;
}
.MusicListImg{
	position:relative;
	overflow:hidden;
	display:inline-block;
	width:75px;
	height:75px;
}
.MusicListImg>image{
	border-radius:5px 0 0 5px;
	display:inline-block;
	width:100%;
	height:100%;
}
.MusicListImg>p{
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
	text-align:center;
}
.MusicListInfo{
	position:relative;
	flex:1;
	padding:5px 10px;
	background:#efefef;
	display:inline-block;
}
.MusicListInfo>h2{
	font-size:13px;
	color:#000;
}
.MusicListInfo>p{
	font-size:14px;
	color:#9DA2A6;
}
.MusicListInfo>span{
	font-size:12px;
	color:#9DA2A6;
}
.MusicListMv{
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
