<template>
	<view class="btnall">
		<view   v-for="(item,index) in resdata.list" :key="index">
			<view class="btn" :class="resdata.selected == index ? 'btnsel':''" @click="changeRadio(index)">
				{{item.name}}
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data(){
			return {
				resdata:this.label,
			}
		},
		props: {
			label: Object,
		},
		methods: {
			changeRadio(index) {
				this.resdata.selected = index;
				// console.log(`第${index}个选项`);
				this.$emit('submig',index)
			}
		},
	}
</script>

<style>
	.btnall{
		display: flex;
		flex-wrap: wrap;
	}
	.btn{
		padding: 20rpx 30rpx;
		background-color: #f7fafa;
		display: flex;
		margin: 20rpx;
		font-size: 25rpx;
		white-space: nowrap;
	}
	.btnsel{
		background-color: #fce1d5;
		border: 3rpx solid #FD6801;
		color: #FD6801;
	}
</style>
