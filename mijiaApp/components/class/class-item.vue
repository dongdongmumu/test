<template>
	<view class="d-flex flex-column " style="height: 200rpx;margin: 20rpx;">
		<view class="">
			<image :src='resdata.src' class="imgStyle" mode=""></image>
		</view>
		<view class="textStyle">
			{{resdata.name}}
		</view>
	</view>
</template>

<script>
	export default{
		props:{
			resdata:Object
		}
	}
</script>

<style>
	.imgStyle{
		width: 120rpx;
		height: 120rpx;
	}
	.textStyle{
		font-size: 27rpx;
	}
</style>
