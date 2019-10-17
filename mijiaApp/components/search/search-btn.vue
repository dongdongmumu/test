<template>
		<view  class="btn" :style="getStyle" >
			{{item.name}}
		</view>
</template>

<script>
	export default {
		props: {
			item:Object,
			color: {
				default: true,
				type: Boolean
			}
		},
		computed: {
			getStyle() {
				if (!this.color) {
					return `background:#f5f5f5;color:#7A7A7A`;
				}
				let color = {
					bc : ['#EEA6AA', '#DD6A4B', '#98D5D8', '#9DBE93', '#BCCD99'],
					bgc : ['#F8EAE9', '#FFBEC6', '#E8F6F6', '#E4F5E2', '#F2F6E8']
				};
				let index = Math.floor(Math.random() * color.bc.length)
				let background = color.bgc[index];
				let borderColor = color.bc[index];
				return `background:${background};border:3rpx solid ${borderColor};`
			}
		}
	}
</script>



<style>
	.btn {
		display: inline-block;
		font-size: 25rpx;
		padding: 20rpx;
		margin: 15rpx;
	}
</style>
