<template>
	<view class="fs" :style="fsize" >
		￥<slot></slot>
	</view>
</template>

<script>
	export default{
		props:{
			fs:{
				default:27
			}
		},
		computed:{
			fsize(){
				return `font-size:${this.fs}rpx;`
			}
			
		}
	}
</script>

<style>
	.fs{
		display: flex;
		color: #FD6801;
		font-style: bold;
	}
</style>
