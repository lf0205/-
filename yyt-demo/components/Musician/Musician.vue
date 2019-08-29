<template>
	<view>
		<view class='Musician'>
			<view class='MusicianTitleLogo'>
				<h2>热门音乐人</h2>
				<p></p>
			</view>
		</view>
		<view class="Musicians">
			<ul>
				<li class='MusiciansList' v-for='(m,i) in MusicianData' :key='i'>
					<view class='MusiciansListImgBox'>
						<image class='MusiciansListImg' :src="m.head_link" mode=""></image>
						<image class='Musicianvip' src='../../static/vip.png'></image>
					</view>
					<p>{{m.nickname}}</p>
					<p>{{m.fans_num}}粉丝</p>
					<view class='follow'>+关注</view>
				</li>
			</ul>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				MusicianData:[]
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
					console.log('热门音乐人数据获取成功:',res.data.data.recommend_musician.musician)
					this.MusicianData = res.data.data.recommend_musician.musician
				},
				fail: () => {},
				complete: () => {}
			});
		}
	}
</script>

<style>
.Musician{
	background: url(../../static/ace05.png) no-repeat;
	background-size: auto 2rem;
	display: flex;
	align-items: center;
	background-position: 0;
	height: 62px;
	padding-left: 40px;
}
.MusicianTitleLogo{
	position: relative;
	display: inline-block;
}
.MusicianTitleLogo>h2{
	font-size:17px;
}
.MusicianTitleLogo>p{
	position: absolute;
	bottom: 3px;
	right: 0;
	width: 44px;
	height: 8px;
	border-radius: 5px;
	background: #ffd9e6;
	z-index: -1;
}
.Musicians>ul{
	list-style: none;
	padding:0;
	display:flex;
	flex-wrap: wrap;
	justify-content: space-between;
}
.MusiciansList{
	margin-bottom:20px;
	display:flex;
	width:30%;
	justify-content:center;
	flex-direction:column;
	align-items:center;
	
}
.MusiciansListImgBox{
	width:85px;
	height:85px;
	position:relative;
}
.MusiciansListImgBox>.Musicianvip{
	position:absolute;
	bottom:0;
	right:0;
	width:16px;
	height:16px;
}
.MusiciansListImg{
	border-radius:50%;
	width:100%;
	height:100%;
	display:inline-block;
}
.MusiciansList>p{
	font-size:13px;
}
.MusiciansList>p:nth-of-type(2){
	font-size:12px;
	color:#9da2a6;
}
.follow{
	width:60px;
	height:25px;
	background:#ff73a1;
	border-radius:15px;
	color:#fff;
	text-align:center;
}
</style>
