<template>
	<view>
		<swiper class="swiper" indicator-dots autoplay interval="2000" duration="1000" circular>
			<block v-for="(item,index) in resdata" :key="index">
				<swiper-item>
					<view class="swiper-item" @click="swiperItem(index)">
						<image :src="item.src" lazy-load style="height: 350rpx;"></image>
					</view>
				</swiper-item>
			</block>
		</swiper>
	</view>
</template>

<script>
	export default {
		props:{
			resdata:Array
		},
		methods: {
			swiperItem(index){
				console.log(index)
			}
		}
	}
</script>

<style>
</style>
