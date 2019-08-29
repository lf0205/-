<template>
	<view class="Apply">
		<view class='ApplyTitle'>
			<view class="ApplyFrom">如果每个人都能理解你，那你得普通成什么样子~</view>
		</view>
		<view class='ApplyLogo' v-for='(Apply,i) in ApplyData' :key='i'>
			<image mode="aspectFill" class="ApplyLogoImg" :src="Apply.imgpic_link"></image>
			<view class='ApplyLogoTitle'>
				<p>{{Apply.place}}</p>
				<p>{{Apply.title}}</p>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				ApplyTitle:'',
				ApplyData:[]
			}
		},
		methods: {
			
		},
		mounted(){
			uni.request({
				url: 'https://www.easy-mock.com/mock/5d5e512adfc6562118918a97/api/yytdata',
				method: 'GET',
				data: {},
				success: res => {
					this.ApplyData = res.data.data.home_ad
					console.log('Apply歌单获取成功:',res.data.data.home_ad)
				},
				fail: () => {},
				complete: () => {}
			});
		}
	}
</script>

<style>
.Apply{
		margin-top: 15px;
	}
	.ApplyTitle{
		background: url(../../static/ace02.png) no-repeat;
		padding:10px 0 10px 50px;
		background-size: auto 3rem;
		display: flex;
		align-items: center;
		background-position: 0;
	}
	.ApplyFrom{
		padding:0 10px;
		margin-left: 5px;
		width: 100%;
		line-height: 32px;
		white-space: nowrap;
		overflow: hidden;
		text-overflow: ellipsis;
		border-radius: 15px;
		background: #EEEEEE;
	}
	::placeholder{
		font-size: 13px;
	}
	.ApplyLogo{
		margin-top: 10px;
		position: relative;
		width:100%;
		height:105px;
	}
	.ApplyLogoImg{
		border-radius: 5px;
		position: absolute;
		top: 0;
		left: 0;
		width: 100%;
		height: 100%;
		z-index: -1;
	}
	.ApplyLogoTitle{
		position: absolute;
		bottom: 10px;
		left: 10px;
		color: #FFFFFF;
		display: flex;
		align-items: center;
	}
	.ApplyLogoTitle>p:nth-of-type(1){
		margin-right:5px;
		border-radius: 5px;
		text-align: center;
		width: 32px;
		line-height: 18px;
		border: 1px solid #FFFFFF;
	}
</style>
