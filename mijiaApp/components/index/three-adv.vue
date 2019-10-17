<template>
	<view>
		<divider></divider>
		<view  class="d-flex flex-row flex-nowrap j-sb" style="height:530rpx;">
			<view class="" @click="even(resdata[0])">
				<image :src="resdata.big.src" lazy-load mode="" style="width: 373rpx;height:530rpx;"></image>
			</view>
			<view class="d-flex flex-column j-sb" style="height: 530rpx;" >
				<image @click="even(resdata[1])" lazy-load :src="resdata.smalltop.src" style="width: 375rpx;height: 264rpx;" mode=""></image>
				<image @click="even(resdata[2])" lazy-load :src="resdata.smallbottom.src" style="width: 375rpx;height: 264rpx;" mode=""></image>
			</view>
		</view>
		<!-- 粗实线 -->
		<divider></divider>
	</view>
</template>

<script>
	import divider from "@/components/common/divider.vue"
	export default{
		props:{
			resdata:Object
		},
		methods:{
			even(data){
				console.log(data.text)
			}
		},
		components:{
			divider
		}
	}
</script>

<style>
</style>
