<template>
	<view class="record">
		{{resdata.name}}
	</view>
</template>

<script>
	export default{
		props:{
			resdata:Object
		},
		methods:{
			
		}
	}
</script>

<style>
	.record{
		display: block;
		height: 90rpx;
		font-size: 30rpx;
		line-height: 90rpx;
		padding-left: 30rpx;
		border-bottom: 2rpx solid #f5f5f5;
	}
</style>
