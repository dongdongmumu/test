<template>
	<view>
		<!-- 轮播图 -->
		<view class="d-block" @click="clickSwipe">
			<swiper :resdata="shopingData.swiper"></swiper>
		</view>
		<view class="px-2">
			<!-- 商品说明 -->
			<view class="d-flex flex-column text-left" style="margin-top: 400rpx;">
				<text style="font-size: 32rpx;">{{shopingData.description.name}}</text>
				<text style="font-size: 23rpx;color: #666666;">{{shopingData.description.text}}</text>
			</view>
			<!-- 价格 -->
			<view class="">
				<price :fs="34">{{shopingData.description.price}}</price>
			</view>
			<!-- 配置 -->
			<scroll-view scroll-x class="iconswp">
				<view v-for="(item,index) in shopingData.configuration" :key="index" class="iconswp-item">
					<icon-swiper :resdata="item"></icon-swiper>
				</view>
			</scroll-view>
			<!-- 三个选项 -->
			<view class="selectPOP">
				<view class="selectPOP-item" @click="showpop">
					<text style="color: #000000;">已选</text> <text>  {{selectColor}}  {{selectCapacity}}  {{selectPackage}}</text><text style="float: right;">></text>
				</view>
				<view class="selectPOP-item" >
					<text style="color: #000000;">配送</text><text></text><text style="float: right;">></text>
				</view>
				<view class="selectPOP-item" >
					<text >大米专卖 小米发货 按时不到</text><text style="float: right;color: #000000;">></text>
				</view>
			</view>
			<!-- 评论轮播图 -->
			<scroll-view scroll-x class="comment-list">
				<!--  -->
				<view class="m-2 comment-item" v-for="(item,index) in shopingData.comment.list" :key="index" >
					<!-- 评论头部信息 -->
					<view class="commment-top d-flex flex-row j-sb">
						<view class="d-flex flex-row a-center" style="height: 120rpx;width: 620rpx;" >
							<view class="">
								<image :src="item.head" mode="" style="width: 120rpx;height: 120rpx;border-radius: 60rpx;"></image>
							</view>
							<view class="d-flex flex-column">
								<text style="font-size: 27rpx;">{{item.name}}</text>
								<text style="color: #acadaa; font-size: 18rpx;">{{item.time}}</text>
							</view>
						</view>
						<view class="d-flex flex-row a-center" style="height: 120rpx;" @click="Addlike(item,index)" :style="islikeYet(item) ? 'color:#FD6801' : '' ">
							<view class="iconfont icon-dianzan" ></view>
							<text>  {{item.like}}</text>
						</view>
					</view>
					<!-- 评论内容 -->
					<view class="d-flex flex-column" style="height: 250rpx;">
						<text style="white-space: pre-wrap;">{{item.description}}</text>
						<view class=" d-flex flex-row flex-nowrap" style="width: 620rpx;justify-content: space-around;">
							<view v-for="(v,i) in item.src" :key="i">
								<image :src="v" mode="" class="comment-img" ></image>
							</view>
						</view>
					</view>
				</view>
			</scroll-view>
			<!-- 底部购物栏 -->
			<view class="basket">
				<view class="d-flex flex-row flex-nowrap" style="background-color: #FFFFFF;width: 100%;">
					<view class="d-flex flex-column text-center a-center" style="width: 23%;" >
						<view class="iconfont icon-xihuan"></view><text>收藏</text>
					</view>
					<view class="d-flex flex-column text-center a-center" style="width: 23%;" >
						<view class="iconfont icon-gouwuche"></view><text>购物车</text>
					</view>
					<view class="" style="width:60%;text-align:center;line-height: 100rpx;background-color: #FD6801;">
						<text style="color: #FFFFFF;">加入购物车</text>
					</view>
				</view>
			</view>
			<!-- 底部弹框 -->
			<view :class=" popdisplay ? 'show' : 'hide' ">
				<pop-box @submig="closePop">
					<card headTitle="颜色">
						<view class="" style="display: flex;">
							<radio-group :label="shopingData.popData.color" @submig="msgA"></radio-group>
						</view>
					</card>
					<card headTitle="容量">
						<view class="" style="display: flex;">
							<radio-group :label="shopingData.popData.capacity" @submig="msgB"></radio-group>
						</view>
					</card>
					<card headTitle="套餐">
						<view class="" style="display: flex;">
							<radio-group :label="shopingData.popData.package" @submig="msgC"></radio-group>
						</view>
					</card>
					<view style="height: 1rpx; background-color: #DEE2E6;"></view>
					<view class="h-100 d-flex j-sb m-2">
						<view style="line-height: 100rpx;display: inline-block;">购买数量</view>
						<view class="d-flex" style="">
							<button class="btn-num" @click="shopNumSub">-</button>
							<view class="btn-num" style="line-height: 100rpx;text-align: center;">{{purchaseNum}}</view>
							<button class="btn-num" @click="shopNumAdd">+</button>
						</view>
					</view>
					<!-- 加入购物车按钮 -->
					<view>
						<button class="add-cart" @click="AddCart">加入购物车</button>
					</view>
				</pop-box>
			</view>
		</view>
	</view>
</template>

<script>
	import swiper from "@/components/productDetail/swiper.vue";
	import price from "@/components/common/price.vue";
	import iconSwiper from "@/components/productDetail/icon-swiper.vue";
	import popBox from "@/components/productDetail/pop-box.vue";
	import radioGroup from "@/components/common/radio-group.vue";
	import card from "@/components/common/card.vue";
	export default {
		components:{
			swiper,price,iconSwiper,popBox,radioGroup,card
		},
		onLoad() {
			this.selectColor = this.shopingData.popData.color.list[0].name,
			this.selectCapacity = this.shopingData.popData.capacity.list[1].name,
			this.selectPackage = this.shopingData.popData.package.list[2].name
		},
		data() {
			return {
				popdisplay:false,
				selectColor:"",
				selectCapacity:"",
				selectPackage:"",
				purchaseNum:1,	//购买数量
				isLike:[],			//是否点过赞
				shopingData:{
					swiper:[
						{"src":"/static/images/demo/list/6.jpg"},
						{"src":"/static/images/demo/list/6.jpg"},
						{"src":"/static/images/demo/list/6.jpg"}
					],
					description:{
						"price":"5555",
						"name":"水水水水水水水水水水水水水",
						"text":"哈哈哈哈哈哈哈哈哈哈哈哈哈哈飒飒水水水水水水水水撒啊啊啊啊啊啊啊啊啊撒啊啊啊啊啊啊啊啊"
					},
					configuration:[
						{"icon":"icon-cpu","name":"CPU","text":"蛟龙845八核"},
						{"icon":"icon-cpu","name":"CPU","text":"蛟龙845八核"},
						{"icon":"icon-cpu","name":"CPU","text":"蛟龙845八核"},
						{"icon":"icon-paishe","name":"CPU","text":"蛟龙845八核"},
						{"icon":"icon-paishe","name":"CPU","text":"蛟龙845八核"},
						{"icon":"icon-paishe","name":"CPU","text":"蛟龙845八核"},
						{"icon":"icon-paishe","name":"CPU","text":"蛟龙845八核"},
						{"icon":"icon-paishe","name":"CPU","text":"蛟龙845八核"},
						{"icon":"icon-paishe","name":"CPU","text":"蛟龙845八核"},
						{"icon":"icon-paishe","name":"CPU","text":"蛟龙845八核"},
					],
					popData:{
						color:{
							selected:0,
							list:[
								{name:"火焰红"},
								{name:"炭黑"},
								{name:"冰川兰"},
							]
						},
						capacity:{
							selected:1,
							list:[
								{name:"64GB"},
								{name:"128GB"},
							]
						},
						package:{
							selected:2,
							list:[
								{name:"标准"},
								{name:"套餐一"},
								{name:"套餐二"},
							]
						}
					},
					comment:{
						list:[
							{head:"/static/images/demo/demo5.jpg",name:"理化生",time:"2019-03-04",like:555,description:"爱哇哇哇哇哇哇哇哇哇哇哇哇哇哇哇哇哇哇飒飒大苏打",src:["/static/images/demo/list/6.jpg","/static/images/demo/list/6.jpg","/static/images/demo/list/6.jpg"]},
							{head:"/static/images/demo/demo5.jpg",name:"理化生",time:"2019-03-04",like:555,description:"爱哇哇哇哇哇哇哇哇哇哇哇哇哇哇哇哇哇哇飒飒大苏打",src:["/static/images/demo/list/6.jpg","/static/images/demo/list/6.jpg"]},
							{head:"/static/images/demo/demo5.jpg",name:"理化生",time:"2019-03-04",like:555,description:"爱哇哇哇哇哇哇哇哇哇哇哇哇哇哇哇哇哇哇飒飒大苏打",src:["/static/images/demo/list/6.jpg","/static/images/demo/list/6.jpg"]},
							{head:"/static/images/demo/demo5.jpg",name:"理化生",time:"2019-03-04",like:555,description:"爱哇哇哇哇哇哇哇哇哇哇哇哇哇哇哇哇哇哇飒飒大苏打",src:["/static/images/demo/list/6.jpg","/static/images/demo/list/6.jpg","/static/images/demo/list/6.jpg"]},
							{head:"/static/images/demo/demo5.jpg",name:"理化生",time:"2019-03-04",like:555,description:"爱哇哇哇哇哇哇哇哇哇哇哇哇哇哇哇哇哇哇飒飒大苏打",src:["/static/images/demo/list/6.jpg","/static/images/demo/list/6.jpg"]},
						]
					}
				},
			}
		},
		methods: {
			// 蒙版显示
			showpop(){
				 if(this.popdisplay == true){
					setTimeout(()=>{
						this.popdisplay = false;
					},500)
				}else if(this.popdisplay == false){
					this.popdisplay = true;
				}
			},
			// 点击蒙版，触发事件，关闭弹框
			closePop(){
				this.popdisplay = false;
			},
			msgA(value){
				console.log(value.target.__args__)
				let index = value.target.__args__;
				this.selectColor = this.shopingData.popData.color.list[index].name
			},
			msgB(value){
				console.log(value.target.__args__)
				let index = value.target.__args__;
				this.selectCapacity = this.shopingData.popData.capacity.list[index].name
			},
			msgC(value){
				console.log(value.target.__args__)
				let index = value.target.__args__;
				this.selectPackage = this.shopingData.popData.package.list[index].name
			},
			//购买数量的加减
			shopNumSub(){
				if(this.purchaseNum>1){this.purchaseNum--}
			},
			shopNumAdd(){
				this.purchaseNum++
			},
			//加入购物车
			AddCart(){
				console.log(this.selectColor,this.selectCapacity,this.selectPackage);
				this.popdisplay = false;
			},
			//点赞
			Addlike(item,index){
				let yet = this.isLike.some((v,i,a)=>{
					return v == item.name;
				})
				if(!yet){
					this.shopingData.comment.list[index].like++;
					this.isLike.push(item.name);
				}else{
					return
				}
			},
			//点赞之后样式改变
			islikeYet(item){
				let yet = this.isLike.some((v,i,a)=>{
					return v == item.name
				})
				if(yet){
					return true
				}else{
					return false
				}
			},
			
		}
	}
</script>

<style>
	.iconswp{
		display: flex;
		flex-direction: row;
		white-space: nowrap;
	}
	.iconswp-item{
		display: inline-block;
		width: 150rpx;
	}
	.selectPOP{
		margin: 20rpx;
		background-color: #f5f6f3;
		border-radius: 20rpx;
	}
	.selectPOP-item{
		font-size: 28rpx;
		padding: 30rpx;
		color: #767a7e;
		border-bottom: 1rpx solid #F4F5F6;
	}
	.btn-num{
		display: inline-block;
		line-height: 100rpx;
		width: 100rpx;
		height: 100rpx;
		background-color: #f8f8f8;
	}
	.add-cart{
		position: fixed;
		left: 0;
		bottom: 0;
		width: 100%;
		height: 140rpx;
		background-color: #FD6801;
		text-align: center;
		line-height: 140rpx;
		color: #FFFFFF;
	}
	/* 弹框显示 */
	.show{
		display: block;
	}
	.hide{
		display: none;
	}
	/* 评论 */
	.comment-list{
		width: 750rpx;
		height: 420rpx;
		white-space: nowrap;
	}
	.comment-item{
		width: 620rpx;
		background-color: #F5F6F3;
		margin: 20rpx;
		padding: 20rpx;
		display: inline-block;
	}
	.comment-img{
		height: 175rpx;
		width: 175rpx;
		border-radius: 20rpx;
	}
	/* 底部购物篮 */
	.basket{
		position: fixed;
		left: 0;
		bottom: 0;
		width: 100%;
		height: 100rpx;
	}
</style>
