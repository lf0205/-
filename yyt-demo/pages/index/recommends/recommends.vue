<template>
	<view>
		<view class="recommendsHeader">
			<view class="recommendsHeaderInfo">
				<h2>{{date}}</h2>
				<p>{{recommends.cate_img.title}}</p>
				<p>{{Tips}}</p>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				recommends:[],
				date:'',
				Tips:'诸君，你喜欢的音乐都被我承包了❥(^_-)'
			}
		},
		methods: {
			
		},
		mounted(){
			uni.request({
				url: 'https://www.easy-mock.com/mock/5d5dee346728653b7c6b3844/today-recommends',
				method: 'GET',
				data: {},
				success: res => {
					console.log(res.data.data)
					this.recommends = res.data.data
					this.date = res.data.data.cate_img.date.slice(5,7)
				},
				fail: () => {},
				complete: () => {}
			});
		}
	}
</script>

<style>
.recommendsHeaderInfo{
	padding:50px 0;
}
</style>
