<template>
	<view class="d-flex flex-wrap j-sb">
		<block v-for="(item,index) in resdata" :key="index">
			<view style="width:372rpx; height:533rpx;" @click="event(item)">
				<view >
					<image :src="item.cover" lazy-load style="width: 100%;height: 370rpx;"></image>
				</view>
				<view class="d-flex flex-column" style="margin-left: 15rpx; ">
					<text style="font-size: 30rpx;">{{item.title}}</text>
					<text style="font-size: 20rpx;color: #b7b7b7;">{{item.desc}}</text>
					<view class="d-flex a-end">
						<view class="d-flex">
							<text style="font-size: 20rpx;color: #FD6801;">￥</text>
							<price>{{item.price}}</price>
						</view>
						<text style="font-size: 17rpx;color: #adadad;padding-left: 20rpx;">￥{{item.oldprice}}</text>
					</view>
				</view>
			</view>
		</block>
	</view>
</template>

<script>
	import price from "@/components/comment/price.vue"
	export default{
		props:{
			resdata:Array
		},
		methods:{
			event(item){
				console.log(item.text)
			}
		},
		components:{
			price
		}
	}
</script>

<style>
</style>
