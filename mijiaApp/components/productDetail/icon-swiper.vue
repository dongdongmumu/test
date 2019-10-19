<template>
	<view class="d-flex flex-column j-center text-center" style="width: 140rpx; ">
		<view class="">
			<view class="iconfont " :class="iconff " ></view>
		</view>
		<text style="font-size: 25rpx;">{{resdata.name}}</text>
		<text style="width: 150rpx;color: #666666;font-size: 19rpx;">{{resdata.text}}</text>
	</view>
</template>

<script>
	export default{
		props:{
			resdata:Object
		},
		computed:{
			iconff(){
				if(!this.resdata.icon){
					return "icon-cpu"
				}
				return `${this.resdata.icon}`
			}
		}
		
	}
</script>

<style>
</style>
