<template>
	<view class="list">
		<view class="listLeft">
			<image :src='item.titlepic' class="listImg"  mode=""></image>
		</view>
		<view class="listRight">
			<view style="font-size: 35rpx; color: black;">{{item.title}}</view>
			<view style="font-size: 26rpx;color: #606c65;">{{item.desc}}</view>
			<price>{{item.pprice}}</price>
			<view style="font-size: 23rpx;color: #606c65;">
				<text>{{item.comment_num}}条评论</text>		<text>{{item.good_num}}满意</text>
			</view>
		</view>
	</view>
</template>

<script>
	import price from "@/components/common/price.vue"
	export default{
		components:{
			price
		},
		props:{
			item:Object
		},
		
	}
</script>

<style>
	.list{
		display: flex;
		flex-direction: row;
		flex-wrap: nowrap;
		height: 250rpx;
		margin: 20rpx;
	}
	.listLeft{
		height: 250rpx;
		width: 280rpx;
		text-align: left;
	}
	.listImg{
		width: 250rpx;
		height: 250rpx;
	}
	.listRight{
		width: 430rpx;
		height: 250rpx;
		display: flex;
		flex-direction: column;
		padding-top: 20rpx;
	}
</style>
