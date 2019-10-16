<template>
	<view>
		<view v-if="showhead" class="p-2">
			<slot name="title">
				<text v-if="headTitle" class="font-md font-weight">{{headTitle}}</text>
			</slot>
		</view>
		<view>
			<image v-if="bodyCover" :src="bodyCover"></image>
			<slot></slot>
		</view>
	</view>
</template>

<script>
	export default {
		props:{
			headTitle:String,
			bodyCover:String,
			showhead:{
				type:Boolean,
				default:true
			}
		}
	}
</script>

<style>

</style>
