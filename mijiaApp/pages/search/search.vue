<template>
	<view>
		<card headTitle="热门搜索" :imgheight="209" bodyCover="../../static/images/demo/search-banner.png"></card>
		<view  class="flexItem">
			<view v-for="(value,index) in hot" :key="index" @click="clickItem(value.name)">
				<search-btn :color="true">{{value.name}}</search-btn>
			</view>
		</view>
		<card headTitle="常用分类" ></card>
		<view class="flexItem" >
			<view v-for="(value,index) in cate" :key="index"  @click="clickItem(value.name)">
				<search-btn >{{value.name}}</search-btn>
			</view>
		</view>
		<divider></divider>
		<card headTitle="搜索记录" ></card>
		<view style="height: 2rpx ;background-color: #f5f5f5;width: 100%;"></view>
		<view>
			<view v-for="(value,index) in searchRecord" :key="index"  @click="clickItem(value.name)" >
				<search-record :resdata="value" ></search-record>
			</view>
		</view>
	</view>
</template>

<script>
	import card from "@/components/common/card.vue";
	// 搜索选项按钮
	import searchBtn from "@/components/search/search-btn.vue";
	// 搜索历史
	import searchRecord from "@/components/search/search-record.vue";
	import divider from "@/components/common/divider.vue";
	export default {
		components:{
			card,searchBtn,searchRecord,divider
		},
		data() {
			return {
				searchText:"",
				hot:[
					{ name:'领券中心' },
					{ name:'Redmi K20' },
					{ name:'RedmiBook 14' },
					{ name:'智能积木 越野四驱车' },
					{ name:'手环 腕带' },
				],
				cate:[
					{ name:'耳机' },
					{ name:'手机' },
					{ name:'音箱' },
					{ name:'手表' },
					{ name:'配件' },
					{ name:'网关/传感器' },
					{ name:'健康' },
					{ name:'酷玩' },
				],
				searchRecord:[
					{name:"小米"},
					{name:"小强"}
				]
			}
		},
		// 监听原生标题栏搜索输入框输入内容变化事件	
		onNavigationBarSearchInputChanged(value){
			// console.log(value)
			this.searchText = value;
		},
		// 监听原生标题栏按钮点击事件，参数为Object
		onNavigationBarButtonTap(){
			let text= this.searchText;
			uni.navigateTo({
				url:`../searchList/searchList?key=${text}`
			})
		},
		// 监听原生标题栏搜索输入框搜索事件，用户点击软键盘上的“搜索”按钮时触发。
		onNavigationBarSearchInputConfirmed(text){
			// console.log(text);
			uni.navigateTo({
				url:`../searchList/searchList?key=${text}`
			})
		},
		methods: {
			clickItem(text){
				uni.navigateTo({
					url:`../searchList/searchList?key=${text}`
				})
			}
		}
	}
</script>

<style>
	.flexItem{
		display: flex;
		flex-wrap: wrap;
	}
</style>
