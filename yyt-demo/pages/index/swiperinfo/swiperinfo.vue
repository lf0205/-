<template>
	<view class="swiperinfobox">
		<view class="swiperinfo" :key="swiperinfo.id">
			<h2 class='swiperinfotitle'>{{swiperinfo.title}}</h2>
			<p class='SwiperInfoNickname'>{{swiperinfo.nickname}}</p>
			<view class='SwiperInfoVadiu'>
				<image class='SwiperInfoImg' :src="swiperinfo.imgpic_link" mode=""></image>
				<audio class='SwiperInfoAudio' :src="swiperinfo.video_link" controls></audio>
			</view>
			<view class='SwiperInfoSongs' :style='{height:songH}'>
				<p v-for='(s,i) in songs' :key='i'>
					{{s}}
				</p>
			</view>
			<span class='SwiperInfoShow' @click='cuts' :style='{transform:transform}'></span>
			<view class='SwiperInfosBox'>
				<view class='SwiperInfos'>
					<h2>
						参与小伙伴
						<i></i>
					</h2>
					<view class='memberbox'>
						<view class='member' v-for='(m,i) in music_type' :key='i'>
							<p class='music_type'>{{m[0].music_type}} :</p>
							<p class='nickname'>{{m[0].nickname}}</p>
							<p class='nickname nickname2' v-if='m[1]'>{{m[1].nickname}}</p>
						</view>
					</view>
				</view>
				<view class='introbox' >
					<p class='intro' :style='{height:h}'>{{swiperinfo.intro}}</p>
					<p class='show' @click='introshow'>{{cut}}</p>
				</view>
			</view>
		</view>
		<view class="swiperbtn">
			<p>下载歌曲</p>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				swiperinfo:[],
				songs:[],
				music_type:[],
				nickname2:[],
				cut:'展开',
				h:'69px',
				songH:'70px',
				transform: 'rotate(0deg)'
			}
		},
		methods: {
			introshow(){
				if(this.h=='69px'){
					this.cut='收起'
					this.h='110px'
				}else{
					this.cut='展开'
					this.h='69px'
				}
				console.log(1);
				console.log(this.cut);
			},
			cuts(){
				if(this.songH == '70px'){
					this.songH = 'auto'
					this.transform = 'rotate(180deg)'
				}else{
					this.transform = 'rotate(0deg)'
					this.songH='70px'
				}
			}
		},
		mounted(){
			uni.request({
				url: 'https://www.easy-mock.com/mock/5d5f366d094e69513db0e52c/yytSwiperData/swiperinfo',
				method: 'GET',
				data: {},
				success: res => {
					this.swiperinfo = res.data.data
					console.log(this.swiperinfo)
					let songs = res.data.data.lyrics_data
					let member = res.data.data.member
					console.log(res.data.data.member)
					
					// 循环得到歌词
					let arr = []
					for(let i in songs){
						let one = songs[i];
						for( let j in one){
							let word = one[j]
							arr.push(word)
						}
					}
					this.songs = arr;
					
					// 循环得到小伙伴
					let arr2 = []
					let arr3 = []
					for(let i in member){
						arr2.push(member[i].member)
						
						if(member[i].member[1]){
							this.nickname2=(member[i].member[1].nickname)
						}
					}
					this.music_type = arr2;
					this.nickname2 = arr3;
					console.log(this.music_type)
				},
				fail: () => {},
				complete: () => {}
			});
		}
	}
</script>

<style>
.swiperinfo{
	overflow:auto;
	display:flex;
	align-items:center;
	padding-bottom: 56px;
	flex-direction:column;
}
.swiperinfotitle{
	font-size:18px;
	color:#2b2b2b;
}
.SwiperInfoNickname{
	font-size:14px;
	color:#9da2a6;
}
.SwiperInfoVadiu{
	display: flex;
	flex-direction: column;
	align-items: center;
	justify-content: center;
	padding:45px 0;
	position:relative;
}
.SwiperInfoImg{
	width:200px;
	height:200px;
	display:inline-block;
	border-radius:50%;
}
.SwiperInfoVadiu>.SwiperInfoAudio{
	position:absolute;
	background-size: cover;
}
.uni-audio-default{
	display: none;
}
.SwiperInfosBox{
	padding:0 15px;
}
.SwiperInfoSongs{
	text-align:center;
	/* width: 100%; */
	overflow-x:auto;
}
.SwiperInfoShow{
	width:100%;
	height:31px;
	display:inline-block;
	background:url('../../../static/base.png') no-repeat center;
	margin:27.5px 0;
	background-size: 20px;
}
.SwiperInfos{
	display: flex;
	flex-direction: column;
	align-items: center;
}
.SwiperInfos>h2{
	display:inline-block;
	text-align:center;
	font-size:17px;
	color:#2b2b2b;
	position:relative;
}
.SwiperInfos>h2>i{
	position:absolute;
	bottom:3px;
	right:0;
	z-index:-1;
	width:44px;
	height:7px;
	background:#ffd9e6;
}
.memberbox{
	display:flex;
	align-items:center;
	flex-direction:column;
	width:100%;
	justify-content:flex-start;
}
.member{
	width:100%;
	height:40px;
	display:flex;
	align-items:center;
	justify-content:flex-start;
}
.music_type{
	font-weight: bold;
	padding:0 10px;
}
.nickname{
	padding:0 15px;
	font-weight:bold;
}
.nickname2{
	border-left:1px solid #ccc;
}
.intro{
	text-indent: 10px;
	overflow: hidden;
	text-overflow: ellipsis;
	display: -webkit-box;
	-webkit-box-orient: vertical;
	/* -webkit-line-clamp: 3;//要保留显示省略的行数 */
}
.show{
	color:#ff6699;
}
input[type = "radio"] {
display: none;
}
.swiperbtn{
	box-shadow: 0 -1px 0.1rem 0 rgba(0,0,0,.05);
	position:fixed;
	bottom:0;
	left:0;
	width:90%;
	text-align:center;
	padding:10px 20px;
	display:block;
	background:#fff;
}
.swiperbtn>p{
	line-height:36px;
	background:#ff6699;
	color:#fff;
	font-size:16px;
	border-radius:20px;
}
</style>
