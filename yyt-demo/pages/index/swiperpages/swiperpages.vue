<template>
	<!-- 轮播详情页面 -->
	<view class='swiperPageBox'>
		<!-- 头部精选推荐 -->
		<view class="swiperSheet">
			<view class="swiperSheetImg">
				<image class='swiperSheetImgs' :src="swiperpagedata.imgpic_link" mode=""></image>
				<p class='iconfont icon-headset'>{{swiperpagedata.counts}}</p>
			</view>
			<view class="swiperSheetInfo">
				<h2>{{swiperpagedata.title}}</h2>
				<view class="swiperSheetInfoNickname">
					<view class="swiperLogoBox">
						<image class='swiperLogo' :src="swiperpagedata.head_link" mode=""></image>
						<image class='swiperVip' src="../../../static/vip.png" mode=""></image>
					</view>
					<span>{{swiperpagedata.nickname}} ></span>
				</view>
				<view class="swiperSheetInfoAssess">
					<p>
						<span class='iconfont icon-fenxiang'></span>
						<span>{{swiperpagedata.collection}}</span>
					</p>
					<p>
						<span class='iconfont icon-xinxi'></span>
						<span>{{swiperpagedata.comment}}</span>
					</p>
					<p>
						<span class='iconfont icon-dianzan_leave'></span>
						<span>{{swiperpagedata.agrees}}</span>
					</p>
				</view>
			</view>
		</view>
		
		<!-- 歌单标签 -->
		<view class="swiperTitle">
			<h2>{{songTitle}}</h2>
			<ul>
				<li class='songTitleList' v-for='(s,i) in swiperpagedata.tags' :key='i'>{{s.title}}</li>
			</ul>
		</view>
		
		<!-- 歌曲列表 -->
		<view class="swiperList">
			<h2>{{songList}} (共{{num}}首)</h2>
			<ul>
				<li class='swiperListLis' v-for='(m,i) in music' :key='i'>
					<view class='swiperListImgs'>
						<image class='swiperListImg' :src="m.imgpic_link"></image>
					</view>
					<view class='swiperListTitle'>
						<h2>{{m.title}}</h2>
						<p><span>{{musiccopy}}</span>{{m.nickname}}</p>
					</view>
					<audio :src="m.video_link" controls></audio>
				</li>
			</ul>
		</view>
		
		<!-- 推荐歌单 -->
		<view class="swiperSongs">
			<h2>{{songCover}}</h2>
			<view class="swiperSongsList">
				<view class='swiperSongsBox' v-for="(r,i) in recommend" :key='i'>
					<view class='swiperSongsBoxImg'>
						<image class="swiperSongsImg" :src="r.imgpic_link"></image>
						<p class='iconfont icon-headset'>{{r.counts}}</p>
					</view>
					<p>{{r.title}}</p>
				</view>
			</view>
		</view>
		
	</view>
</template>

<script>
	export default {
		data() {
			return {
				id:'',
				swiperpagedata:[],
				songTitle:'歌单标签',
				songList:'歌曲列表',
				songCover:'推荐的歌单',
				num:'',
				music:[],
				musiccopy:'原创',
				recommend:[]
			}
		},
		methods: {
			
		},
		// 通过使用onLoad:func(option)来接收到传过来的数据,(option)就是id的结果
		// 可以保存起来
		onLoad: function (option) {
			// console.log(option);
			this.id = option.id
			if(this.id==1){
				uni.request({
					url: 'https://www.easy-mock.com/mock/5d5dee346728653b7c6b3844/swiperpage1',
					method: 'GET',
					success: res => {
						console.log(res)
						this.swiperpagedata = res.data.data
						this.num = res.data.data.music.length
						this.music = res.data.data.music
						this.recommend = res.data.data.recommend
						// console.log(this.swiperpagedata)
						console.log(this.music)
					}
				});
			}else if(this.id==2){
				uni.request({
					url: 'https://www.easy-mock.com/mock/5d5dee346728653b7c6b3844/swiperpage2',
					method: 'GET',
					success: res => {
						console.log(res)
						this.swiperpagedata = res.data.data
						this.num = res.data.data.music.length
						this.music = res.data.data.music
						this.recommend = res.data.data.recommend
						// console.log(this.swiperpagedata)
						console.log(this.music)
					}
				});
			}
			
			console.log(this.id);
		},
		mounted(){
			// uni.request({
			// 	// url: 'https://www.easy-mock.com/mock/5d5dee346728653b7c6b3844/swiperpages',
			// 	url:'https://www.easy-mock.com/mock/5d5dee346728653b7c6b3844/swiperpage',
			// 	method: 'GET',
			// 	success: res => {
			// 		// console.log(res.data.data.shuffling[this.id].url)
			// 		console.log(res)
			// 	},
			// })
		}
	}
</script>

<style>
	/* 歌单页面 */
.swiperPageBox{
	padding:0 10px;
}

/* 头部精选推荐 */
.swiperSheet{
	background-image: -webkit-linear-gradient(top,hsla(0,0%,100%,.65),hsla(0,0%,100%,.95) 40%,#fff);
	padding:14.5px 0;
	border-bottom:1px solid #000;
	overflow:hidden;
	height:155px;
}
/* 头部精选推荐左侧图片 */
.swiperSheetImg{
	height:100%;
	overflow:hidden;
	position:relative;
	width:45%;
	float:left;
}
.swiperSheetImg>.swiperSheetImgs{
	border-radius:5px;
	width:100%;
	height:100%;
}
/* 头部精选推荐播放量 */
.swiperSheetImg>p{
	position:absolute;
	bottom:10px;
	left:10px;
	color:#fff;
}
/* 头部精选推荐信息 */
.swiperSheetInfo{
	height:100%;
	overflow:hidden;
	width:55%;
	float:left;
	display: flex;
	flex-direction: column;
	align-items: center;
	justify-content: space-between;
}
.swiperSheetInfo>h2{
	font-size:16px;
	color:#1a1717;
}
.swiperSheetInfoNickname{
	width:100%;
	display:flex;
	justify-content:space-around;
}
.swiperSheetInfoNickname>.swiperLogoBox{
	position:relative;
}
.swiperSheetInfoNickname>span{
	display:inline-block;
	fpnt-size:14px;
	color:#9da2a6;
}
.swiperSheetInfo>.swiperSheetInfoNickname>.swiperLogoBox>.swiperLogo{
	width:23px;
	height:23px;
	border-radius:50%;
}
.swiperVip{
	position:absolute;
	width:8px;
	height:8px;
	bottom:5px;
	right:0;
}
.swiperSheetInfoAssess{
	display:flex;
	justify-content:space-around;
	width:100%;
}
.swiperSheetInfoAssess>p{
	color:#9da2a6;
	font-size:12px;
	display: flex;
	flex-direction: column;
	align-items: center;
}
.icon-fenxiang,.icon-xinxi,.icon-dianzan_leave{
	font-size:24px;
}

/* 歌曲标签 */
.swiperTitle{
	padding:15px 0;
	border-bottom:1px solid #eee;
}
.swiperTitle>h2{
	font-size:14px;
	margin-bottom:10px;
	line-height:16px;
	font-weight:400;
}
ul{
	list-style:none;
	padding:0;
}
.songTitleList{
	display: inline-block;
	padding: 6px 14px;
	margin: 5px 5px 0 0;
	background:#f7f7fa;
	color:#9da2a6;
	border-radius:5px;
}
.swiperList{
	padding-top: 10px;
}
.swiperList>h2{
	font-weight: 400;
	font-size:14px;
	margin: 0 0 14px;
}
.swiperList>ul{
	border-top: 2px solid #BEBEBE;
	padding-top:14px;
}
.swiperListLis{
	position:relative;
	padding-top:10px;
	display:flex;
	height:58px;
	overflow:hidden;
}
.swiperListLis>.swiperListTitle{
	position:relative;
	padding-right:48px;
	margin-left:10px;
	border-bottom: 1px solid #ebebeb;
	flex:1;
}
.swiperListLis>.swiperListTitle>h2{
	/* 省略文本(3条) */
	white-space: nowrap;
	overflow: hidden;
	text-overflow: ellipsis;	
	color:#2b2b2b;
	font-size:14px;
	margin-bottom:5px;
}
.swiperListLis>.swiperListTitle>p>span{
	padding:0 3px;
	margin-right:3px;
	border:1px solid #ff6699;
	border-radius:5px;
	color:#ff6699;
}
.swiperListLis>.swiperListTitle>p{
	font-size:12px;
	color:#9da2a6;
}
.swiperListImg{
	width:58px;
	height:58px;
	display:inline-block;
}
.swiperListLis>audio{
	z-index:1;
	position:absolute;
	right: 0px;
	bottom: 0px;
}

/* 推荐的歌单 */
.swiperSongs{
	padding:22px 0 10px;
}
.swiperSongs>h2{
	font-size:14px;
	margin-bottom:10px;
	font-weight: 400;
	color: #2b2b2b;
}

/* kkkkkkkk */
.swiperSongsList{
		display: flex;
		justify-content: space-between;
		flex-wrap: wrap;
	}
	.swiperSongsBox{
		margin-bottom: 10px;
		width:107px;
		height: 150px;
	}
	.swiperSongsBox>p{
		margin-top:5px;
		font-size: 12px;
	}
	.swiperSongsBoxImg{
		width:90px;
		padding-right: 14px;
		height: 90px;
		background: url(../../../static/cj.png) no-repeat 100%;
		background-size: .64rem 100%;
		position: relative;
	}
	.swiperSongsBoxImg>p{
		position: absolute;
		bottom: 0;
		right: 20px;
		color: #FFFDEF;
		font-size: 12px;
		z-index: 2;
	}
	.swiperSongsImg{
		border: 1px solid #EEEEEE;
		border-radius: 5px;
		width: 100%;
		height: 100%;
	}
</style>
