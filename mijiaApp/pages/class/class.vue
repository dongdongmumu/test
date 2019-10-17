<template>
	<view class="">
		<view class="nav">
			<scroll-view class="nav-left" scroll-y :style="'height:'+height+'px'" >
				<view  :class="index==categoryActive?'active':''" v-for="(item,index) in categoryList" :key="index" class="nav-left-item"
				@click="categoryClickMain(item,index)"	>
					{{item.name}}
				</view>
			</scroll-view>
			<scroll-view class="nav-right" scroll-y :style="'height:'+height+'px'" scroll-top="200">
					<view class="" style="display: flex;flex-wrap: wrap;">
						<view v-for="(item,index) in categoryList[categoryActive].subCategoryList" :key="index" class="nav-right-item" @click="shopItem(item)">
							<class-item :resdata="item"></class-item>
						</view>
					</view>
			</scroll-view>
		</view>
	</view>
</template>

<script>
	// <class-item :resdata="v"></class-item>
	import classItem from "@/components/class/class-item.vue";
	export default {
		components:{
			classItem
		},
		data() {
			return {
				selectId:"",
				categoryList: [],
				subCategoryList: [],	//每个分类名都对应着分类列表项
				height: 0,				//屏幕高度
				categoryActive: 0,		//当前选中的分类
				scrollTop:0,			
				scrollHeight: 0,
				classData:[
					{ src:"/static/images/demo/cate_01.png" },
					{ src:"/static/images/demo/cate_02.png" },
					{ src:"/static/images/demo/cate_03.png" },
					{ src:"/static/images/demo/cate_04.png" },
					{ src:"/static/images/demo/cate_05.png" },
					{ src:"/static/images/demo/cate_06.png" },
					{ src:"/static/images/demo/cate_07.png" },
					{ src:"/static/images/demo/cate_08.png" },
					{ src:"/static/images/demo/cate_09.png" },
				]
			}
		},
		methods: {
			scroll(e) {
				this.scrollHeight = e.detail.scrollHeight;
			},
			categoryClickMain(value, index) {
				this.categoryActive = index;
			},
			shopItem(item){
				console.log(item.name)
			},
			getCategory() {
				let index;
				for (var i = 1; i < 16; i++) {
					var subList = [];
					for (var j = 1; j < 21; j++) {
						index = Math.floor(Math.random()*9);
						subList.push({
							"name": i + ":商品" + j,
							"src": this.classData[index].src
						})
					}
					this.categoryList.push({
						"name": "分类" + i,
						"id":i,
						"subCategoryList": subList
					})
				}
				this.subCategoryList = this.categoryList[0].subCategoryList;
			}
		},
		onLoad: function () {
			this.getCategory();
			this.height = uni.getSystemInfoSync().windowHeight;	//获取屏幕高度
		}
	}
</script>

<style>
	.page-body {
		display: flex;
	}
	.nav {
		display: flex;
		width: 100%;
	}
	.nav-left {
		width:20%;
	}
	.nav-left-item {
		height: 100upx;
		border-right: solid 1px #E0E0E0;
		border-bottom: solid 1px #E0E0E0;
		font-size: 30upx;
		display: flex;
		align-items: center;
		justify-content: center;
	}
	.nav-right {
		width: 80%;
	}
	.rightNav{
		display: flex;
		flex-wrap: wrap;
		flex-direction: column;
	}
	.nav-right-item {
		width: 28%;
		height: 220upx;
		float: left;
		text-align: center;
		padding: 11upx;
		font-size: 28upx;
	}
	.nav-right-item image {
		width: 100upx;
		height: 100upx;
	}
	.active {
		color: #FD6801;
		border-left:10rpx solid #FD6801;
	}
</style>
