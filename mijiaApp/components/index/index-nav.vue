<template>
	<view class="d-flex flex-row j-center flex-wrap" style="margin: 33rpx 0;">
		<block v-for="(item,index) in resdata" :key="index">
			<view  class="span-4 d-flex flex-column j-center a-center py-1" @click="event(item)">
				<image :src="item.src" style="width: 60rpx;height: 60rpx;" mode="widthFix"></image>
				<text>{{item.text}}</text>
			</view>
		</block>
	</view>
</template>

<script>
	export default{
		props:{
			resdata:Array
		},
		methods:{
			event(item){
				console.log(item.text)
			}
		}
	}
</script>

<style>
</style>
