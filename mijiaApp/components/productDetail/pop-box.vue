<template>
	<view class="">
		<view class="bg-style" @click="adws" ></view>
		<view class="pop-box">
			<slot></slot>
		</view>
	</view>
</template>

<script>
	export default{
		data(){
			return{
				show:true
			}
		},
		methods:{
			adws(){
				this.$emit("submig")
			}
		}
	}
</script>

<style>
	.show{
		display: block;
		z-index: 999;
	}
	.noshow{
		display: none;
	}
	.bg-style{
		position: fixed;
		left: 0;
		right: 0;
		top: 0;
		bottom: 0;
		background-color: rgba(0,0,0,0.4);
		width: 100%;
		height: 100%;
	}
	.pop-box{
		position: fixed;
		bottom: 0;
		left: 0;
		height: 70%;
		width: 750rpx;
		background-color: #FFFFFF;
	}
</style>
