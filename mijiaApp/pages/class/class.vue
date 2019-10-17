<template>
	<view class="container">
		<view class="page-body">
			<scroll-view class="nav-left" scroll-y :style="'height:'+height+'px'" >
				<view class="nav-left-item" @click="categoryClickMain(item,index)" :key="index" :class="index==categoryActive?'active':''"
				    v-for="(item,index) in categoryList">
					{{item.name}}
				</view>
			</scroll-view>
			<scroll-view class="nav-right" scroll-y :scroll-top="scrollTop" @scroll="scroll" 
				scroll-into-view="selectId" :style="'height:'+height+'px'" scroll-with-animation>
				<!-- 在这里使用循环左侧分类的方式来代表右侧的数据 -->
				
					<view :id="index===0?'first':''" class="nav-right-item" v-for="(item,index) in subCategoryList" :key="index">
						<image :src="item.LOGO" lazy-load/>
						<view>{{item.name}}</view>
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
				height: 0,
				categoryActive: 0,
				scrollTop: 0,
				scrollHeight: 0,
				classData:[
					{ src:"/static/images/demo/cate_01.png",text:"产品说明"},
					{ src:"/static/images/demo/cate_02.png",text:"产品说明" },
					{ src:"/static/images/demo/cate_03.png",text:"产品说明" },
					{ src:"/static/images/demo/cate_04.png",text:"产品说明" },
					{ src:"/static/images/demo/cate_05.png",text:"产品说明" },
					{ src:"/static/images/demo/cate_06.png",text:"产品说明" },
					{ src:"/static/images/demo/cate_07.png",text:"产品说明" },
					{ src:"/static/images/demo/cate_08.png",text:"产品说明" },
					{ src:"/static/images/demo/cate_09.png",text:"产品说明" },
				]
			}
		},
		methods: {
			scroll(e) {
				this.scrollHeight = e.detail.scrollHeight;
			},
			categoryClickMain(categroy, index) {
				this.categoryActive = index;
				this.subCategoryList = categroy.subCategoryList;
				this.scrollTop = -this.scrollHeight * index;
				this.selectId = categroy.id;
			},
			getCategory() {
				let index;
				for (var i = 1; i < 21; i++) {
					var subList = [];
					for (var j = 1; j < 31; j++) {
						index = Math.floor(Math.random()*9);
						subList.push({
							"name": "分类" + i + ":商品" + j,
							"LOGO": this.classData[index].src
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
			this.height = uni.getSystemInfoSync().windowHeight;
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
		width:165rpx;
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
		width: 70%;
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
